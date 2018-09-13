---
title: 'Tutorial: Azure Active Directory integration with Predictix Price Reporting | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Predictix Price Reporting.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 9e9d87e9e211214eb4027cb656844386df4a2f35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554496"
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="1b660-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="1b660-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>
<span data-ttu-id="1b660-104">In this tutorial, you learn how to integrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b660-104">In this tutorial, you learn how to integrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b660-105">Integrating Predictix Price Reporting with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1b660-105">Integrating Predictix Price Reporting with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1b660-106">You can control in Azure AD who has access to Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="1b660-106">You can control in Azure AD who has access to Predictix Price Reporting</span></span>
* <span data-ttu-id="1b660-107">You can enable your users to automatically get signed-on to Predictix Price Reporting (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1b660-107">You can enable your users to automatically get signed-on to Predictix Price Reporting (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="1b660-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1b660-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1b660-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b660-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b660-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b660-110">Prerequisites</span></span>
<span data-ttu-id="1b660-111">To configure Azure AD integration with Predictix Price Reporting, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1b660-111">To configure Azure AD integration with Predictix Price Reporting, you need the following items:</span></span>

* <span data-ttu-id="1b660-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1b660-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1b660-113">A Predictix Price Reporting single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1b660-113">A Predictix Price Reporting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b660-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1b660-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1b660-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1b660-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1b660-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1b660-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1b660-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b660-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b660-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="1b660-118">Scenario Description</span></span>
<span data-ttu-id="1b660-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1b660-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1b660-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b660-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b660-121">Adding Predictix Price Reporting from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b660-121">Adding Predictix Price Reporting from the gallery</span></span>
2. <span data-ttu-id="1b660-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b660-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-the-gallery"></a><span data-ttu-id="1b660-123">Adding Predictix Price Reporting from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b660-123">Adding Predictix Price Reporting from the gallery</span></span>
<span data-ttu-id="1b660-124">To configure the integration of Predictix Price Reporting into Azure AD, you need to add Predictix Price Reporting from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1b660-124">To configure the integration of Predictix Price Reporting into Azure AD, you need to add Predictix Price Reporting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b660-125">**To add Predictix Price Reporting from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b660-125">**To add Predictix Price Reporting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b660-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b660-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Applications][1]

2. <span data-ttu-id="1b660-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1b660-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1b660-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1b660-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="1b660-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1b660-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="1b660-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1b660-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="1b660-135">In the search box, type **Predictix Price Reporting**.</span><span class="sxs-lookup"><span data-stu-id="1b660-135">In the search box, type **Predictix Price Reporting**.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_01.png)

7. <span data-ttu-id="1b660-137">In the results pane, select **Predictix Price Reporting**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1b660-137">In the results pane, select **Predictix Price Reporting**, and then click **Complete** to add the application.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b660-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b660-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b660-140">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b660-140">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b660-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Price Reporting is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b660-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Price Reporting is to a user in Azure AD.</span></span> <span data-ttu-id="1b660-142">In other words, a link relationship between an Azure AD user and the related user in Predictix Price Reporting needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1b660-142">In other words, a link relationship between an Azure AD user and the related user in Predictix Price Reporting needs to be established.</span></span>

<span data-ttu-id="1b660-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="1b660-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Predictix Price Reporting.</span></span>

<span data-ttu-id="1b660-144">To configure and test Azure AD single sign-on with Predictix Price Reporting, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b660-144">To configure and test Azure AD single sign-on with Predictix Price Reporting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b660-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1b660-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b660-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b660-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b660-147">**[Creating a Predictix Price Reporting test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Price Reporting that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1b660-147">**[Creating a Predictix Price Reporting test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Price Reporting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1b660-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b660-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b660-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1b660-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b660-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1b660-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="1b660-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Predictix Price Reporting application.</span><span class="sxs-lookup"><span data-stu-id="1b660-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="1b660-152">**To configure Azure AD single sign-on with Predictix Price Reporting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b660-152">**To configure Azure AD single sign-on with Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="1b660-153">In the classic portal, on the **Predictix Price Reporting** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1b660-153">In the classic portal, on the **Predictix Price Reporting** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="1b660-155">On the **How would you like users to sign on to Predictix Price Reporting** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b660-155">On the **How would you like users to sign on to Predictix Price Reporting** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_03.png) 

3. <span data-ttu-id="1b660-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b660-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_04.png) 
   
    <span data-ttu-id="1b660-159">a.</span><span class="sxs-lookup"><span data-stu-id="1b660-159">a.</span></span> <span data-ttu-id="1b660-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Predictix Price Reporting application using the following pattern: `https://<company name-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="1b660-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Predictix Price Reporting application using the following pattern: `https://<company name-pricing>.predictix.com/sso/request`</span></span>
   
    <span data-ttu-id="1b660-161">b.</span><span class="sxs-lookup"><span data-stu-id="1b660-161">b.</span></span> <span data-ttu-id="1b660-162">click **Next**</span><span class="sxs-lookup"><span data-stu-id="1b660-162">click **Next**</span></span>

4. <span data-ttu-id="1b660-163">On the **Configure single sign-on at Predictix Price Reporting** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b660-163">On the **Configure single sign-on at Predictix Price Reporting** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_05.png)
   
    <span data-ttu-id="1b660-165">a.</span><span class="sxs-lookup"><span data-stu-id="1b660-165">a.</span></span> <span data-ttu-id="1b660-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b660-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="1b660-167">b.</span><span class="sxs-lookup"><span data-stu-id="1b660-167">b.</span></span> <span data-ttu-id="1b660-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b660-168">Click **Next**.</span></span>

5. <span data-ttu-id="1b660-169">To get SSO configured for your application, contact Predictix Price Reporting support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="1b660-169">To get SSO configured for your application, contact Predictix Price Reporting support team and provide them with the following:</span></span>
   
    <span data-ttu-id="1b660-170">• The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="1b660-170">• The downloaded certificate</span></span>
   
    <span data-ttu-id="1b660-171">• The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="1b660-171">• The **Entity ID**</span></span>
   
    <span data-ttu-id="1b660-172">• The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="1b660-172">• The **SAML SSO URL**</span></span>
   
    <span data-ttu-id="1b660-173">• The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="1b660-173">• The **Single Sign Out Service URL**</span></span>

6. <span data-ttu-id="1b660-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b660-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="1b660-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1b660-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b660-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b660-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b660-179">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b660-179">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1b660-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b660-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b660-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b660-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1b660-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1b660-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1b660-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1b660-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b660-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1b660-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1b660-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b660-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="1b660-191">a.</span><span class="sxs-lookup"><span data-stu-id="1b660-191">a.</span></span> <span data-ttu-id="1b660-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1b660-192">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="1b660-193">b.</span><span class="sxs-lookup"><span data-stu-id="1b660-193">b.</span></span> <span data-ttu-id="1b660-194">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b660-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="1b660-195">c.</span><span class="sxs-lookup"><span data-stu-id="1b660-195">c.</span></span> <span data-ttu-id="1b660-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b660-196">Click **Next**.</span></span>

6. <span data-ttu-id="1b660-197">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="1b660-197">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_06.png)</span></span> 
   
    <span data-ttu-id="1b660-198">a.</span><span class="sxs-lookup"><span data-stu-id="1b660-198">a.</span></span> <span data-ttu-id="1b660-199">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1b660-199">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="1b660-200">b.</span><span class="sxs-lookup"><span data-stu-id="1b660-200">b.</span></span> <span data-ttu-id="1b660-201">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b660-201">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="1b660-202">c.</span><span class="sxs-lookup"><span data-stu-id="1b660-202">c.</span></span> <span data-ttu-id="1b660-203">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b660-203">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="1b660-204">d.</span><span class="sxs-lookup"><span data-stu-id="1b660-204">d.</span></span> <span data-ttu-id="1b660-205">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1b660-205">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="1b660-206">e.</span><span class="sxs-lookup"><span data-stu-id="1b660-206">e.</span></span> <span data-ttu-id="1b660-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b660-207">Click **Next**.</span></span>

7. <span data-ttu-id="1b660-208">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1b660-208">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1b660-210">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b660-210">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="1b660-212">a.</span><span class="sxs-lookup"><span data-stu-id="1b660-212">a.</span></span> <span data-ttu-id="1b660-213">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1b660-213">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="1b660-214">b.</span><span class="sxs-lookup"><span data-stu-id="1b660-214">b.</span></span> <span data-ttu-id="1b660-215">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1b660-215">Click **Complete**.</span></span>   

### <a name="creating-an-predictix-price-reporting-test-user"></a><span data-ttu-id="1b660-216">Creating an Predictix Price Reporting test user</span><span class="sxs-lookup"><span data-stu-id="1b660-216">Creating an Predictix Price Reporting test user</span></span>
<span data-ttu-id="1b660-217">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="1b660-217">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="1b660-218">Please work with Predictix Price Reporting support team to add the users in the Predictix Price Reporting platform.</span><span class="sxs-lookup"><span data-stu-id="1b660-218">Please work with Predictix Price Reporting support team to add the users in the Predictix Price Reporting platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b660-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b660-219">Assigning the Azure AD test user</span></span>
<span data-ttu-id="1b660-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="1b660-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Predictix Price Reporting.</span></span>

![Assign User][200] 

<span data-ttu-id="1b660-222">**To assign Britta Simon to Predictix Price Reporting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b660-222">**To assign Britta Simon to Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="1b660-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1b660-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="1b660-225">In the applications list, select **Predictix Price Reporting**.</span><span class="sxs-lookup"><span data-stu-id="1b660-225">In the applications list, select **Predictix Price Reporting**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_50.png) 

3. <span data-ttu-id="1b660-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1b660-227">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="1b660-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b660-229">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="1b660-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1b660-230">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="1b660-232">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1b660-232">Testing Single Sign-On</span></span>
<span data-ttu-id="1b660-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1b660-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b660-234">When you click the Predictix Price Reporting tile in the Access Panel, you should get automatically signed-on to your Predictix Price Reporting application.</span><span class="sxs-lookup"><span data-stu-id="1b660-234">When you click the Predictix Price Reporting tile in the Access Panel, you should get automatically signed-on to your Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b660-235">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="1b660-235">Additional Resources</span></span>
* [<span data-ttu-id="1b660-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b660-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b660-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b660-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_205.png

























