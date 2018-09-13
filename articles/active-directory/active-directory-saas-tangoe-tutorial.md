---
title: 'Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tangoe Command Premium Mobile.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: ffeb4adacb66a0980eccefe4a6d1e532249f3862
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554411"
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="d3a78-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="d3a78-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="d3a78-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3a78-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3a78-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d3a78-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d3a78-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="d3a78-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
* <span data-ttu-id="d3a78-107">You can enable your users to automatically get signed on to Tangoe Command Premium Mobile single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d3a78-107">You can enable your users to automatically get signed on to Tangoe Command Premium Mobile single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d3a78-108">You can manage your accounts in one central location with the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d3a78-108">You can manage your accounts in one central location with the Azure classic portal</span></span>

<span data-ttu-id="d3a78-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3a78-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3a78-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3a78-110">Prerequisites</span></span>
<span data-ttu-id="d3a78-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d3a78-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

* <span data-ttu-id="d3a78-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d3a78-112">An Azure subscription</span></span>
* <span data-ttu-id="d3a78-113">A Tangoe Command Premium Mobile single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d3a78-113">A Tangoe Command Premium Mobile single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d3a78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d3a78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="d3a78-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d3a78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d3a78-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d3a78-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d3a78-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3a78-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3a78-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="d3a78-118">Scenario Description</span></span>
<span data-ttu-id="d3a78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d3a78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="d3a78-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3a78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3a78-121">Adding Tangoe Command Premium Mobile from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3a78-121">Adding Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="d3a78-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d3a78-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="d3a78-123">Adding Tangoe Command Premium Mobile from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3a78-123">Adding Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="d3a78-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d3a78-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3a78-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3a78-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3a78-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d3a78-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d3a78-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d3a78-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d3a78-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d3a78-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d3a78-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d3a78-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d3a78-135">In the search box, type **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-135">In the search box, type **Tangoe Command Premium Mobile**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_01.png)
7. <span data-ttu-id="d3a78-137">In the results pane, select **Tangoe Command Premium Mobile**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d3a78-137">In the results pane, select **Tangoe Command Premium Mobile**, and then click **Complete** to add the application.</span></span>

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3a78-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3a78-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d3a78-140">In this section, you configure and test Azure AD SSO with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3a78-140">In this section, you configure and test Azure AD SSO with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3a78-141">For SSO to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3a78-141">For SSO to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="d3a78-142">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d3a78-142">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="d3a78-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="d3a78-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tangoe Command Premium Mobile.</span></span>

<span data-ttu-id="d3a78-144">To configure and test Azure AD SSO with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3a78-144">To configure and test Azure AD SSO with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3a78-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d3a78-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3a78-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3a78-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3a78-147">**[Creating an Tangoe Command Premium Mobile test user](#creating-an-tangoe-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d3a78-147">**[Creating an Tangoe Command Premium Mobile test user](#creating-an-tangoe-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d3a78-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3a78-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3a78-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d3a78-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3a78-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3a78-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="d3a78-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Tangoe Command Premium Mobile application.</span><span class="sxs-lookup"><span data-stu-id="d3a78-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="d3a78-152">**To configure Azure AD SSO with Tangoe Command Premium Mobile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3a78-152">**To configure Azure AD SSO with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="d3a78-153">In the classic portal, on the **Tangoe Command Premium Mobile** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3a78-153">In the classic portal, on the **Tangoe Command Premium Mobile** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="d3a78-155">On the **How would you like users to sign on to Tangoe Command Premium Mobile** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-155">On the **How would you like users to sign on to Tangoe Command Premium Mobile** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_03.png) 
3. <span data-ttu-id="d3a78-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3a78-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_04.png) 

   1. <span data-ttu-id="d3a78-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Tangoe Command Premium Mobile application using the following pattern: **“https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=\<tenant issuer\>&Target=\<target page URL\>”**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Tangoe Command Premium Mobile application using the following pattern: **“https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=\<tenant issuer\>&Target=\<target page URL\>”**.</span></span>

   2. <span data-ttu-id="d3a78-160">In the **Reply URL** textbox, type the URL in the following pattern: **"https://sso.tangoe.com/sp/ACS.saml2"**</span><span class="sxs-lookup"><span data-stu-id="d3a78-160">In the **Reply URL** textbox, type the URL in the following pattern: **"https://sso.tangoe.com/sp/ACS.saml2"**</span></span>

     >[!NOTE]  
     ><span data-ttu-id="d3a78-161">If you don't know the correct values for the URLs, you can use the values above as placeholders and request the the correct values from your Tangoe customer support associate.</span><span class="sxs-lookup"><span data-stu-id="d3a78-161">If you don't know the correct values for the URLs, you can use the values above as placeholders and request the the correct values from your Tangoe customer support associate.</span></span>
     >

4. <span data-ttu-id="d3a78-162">On the **Configure single sign-on at Tangoe Command Premium Mobile** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3a78-162">On the **Configure single sign-on at Tangoe Command Premium Mobile** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_05.png) 
  1. <span data-ttu-id="d3a78-164">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d3a78-164">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d3a78-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-165">Click **Next**.</span></span>

5. <span data-ttu-id="d3a78-166">To get SSO configured for your application, contact your Tangoe customer support associate and provide the following:</span><span class="sxs-lookup"><span data-stu-id="d3a78-166">To get SSO configured for your application, contact your Tangoe customer support associate and provide the following:</span></span>

   - <span data-ttu-id="d3a78-167">The downloaded metadata file</span><span class="sxs-lookup"><span data-stu-id="d3a78-167">The downloaded metadata file</span></span>
   - <span data-ttu-id="d3a78-168">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="d3a78-168">The **Issuer URL**</span></span>
   - <span data-ttu-id="d3a78-169">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="d3a78-169">The **SAML SSO URL**</span></span>
   - <span data-ttu-id="d3a78-170">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="d3a78-170">The **Single Sign-Out Service URL**</span></span>

6. <span data-ttu-id="d3a78-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="d3a78-173">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-173">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3a78-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3a78-175">Create an Azure AD test user</span></span>
<span data-ttu-id="d3a78-176">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3a78-176">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

* <span data-ttu-id="d3a78-177">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-177">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d3a78-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3a78-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3a78-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="d3a78-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d3a78-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d3a78-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-183">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d3a78-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="d3a78-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3a78-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="d3a78-189">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d3a78-189">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="d3a78-190">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-190">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d3a78-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-191">Click **Next**.</span></span>
6. <span data-ttu-id="d3a78-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3a78-192">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_06.png) 
   
  1. <span data-ttu-id="d3a78-194">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-194">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d3a78-195">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-195">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d3a78-196">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d3a78-197">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-197">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d3a78-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-198">Click **Next**.</span></span>
7. <span data-ttu-id="d3a78-199">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-199">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d3a78-201">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3a78-201">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/create_aaduser_08.png) 
   
  1. <span data-ttu-id="d3a78-203">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-203">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="d3a78-204">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-204">Click **Complete**.</span></span>   

### <a name="create-an-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="d3a78-205">Create an Tangoe Command Premium Mobile test user</span><span class="sxs-lookup"><span data-stu-id="d3a78-205">Create an Tangoe Command Premium Mobile test user</span></span>
<span data-ttu-id="d3a78-206">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="d3a78-206">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="d3a78-207">Tangoe Command Premium Mobile application need all the users to be provisioned in the application before doing Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="d3a78-207">Tangoe Command Premium Mobile application need all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="d3a78-208">So please work with the Tangoe Customer support associate to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="d3a78-208">So please work with the Tangoe Customer support associate to provision all these users into the application.</span></span> 

>[!NOTE]
><span data-ttu-id="d3a78-209">If you need to create a user manually or batch of users, you need to contact the Tangoe Command Premium Mobile support team.</span><span class="sxs-lookup"><span data-stu-id="d3a78-209">If you need to create a user manually or batch of users, you need to contact the Tangoe Command Premium Mobile support team.</span></span>
>
>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3a78-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3a78-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="d3a78-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="d3a78-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Tangoe Command Premium Mobile.</span></span>

![Assign User][200] 

<span data-ttu-id="d3a78-213">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3a78-213">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="d3a78-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d3a78-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

 ![Assign User][201] 

2. <span data-ttu-id="d3a78-216">In the applications list, select **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-216">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

 ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_50.png) 
 
3. <span data-ttu-id="d3a78-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-218">In the menu on the top, click **Users**.</span></span>

 ![Assign User][203] 

4. <span data-ttu-id="d3a78-220">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-220">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d3a78-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d3a78-221">In the toolbar on the bottom, click **Assign**.</span></span>

![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d3a78-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3a78-223">Test single sign-on</span></span>
<span data-ttu-id="d3a78-224">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d3a78-224">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d3a78-225">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span><span class="sxs-lookup"><span data-stu-id="d3a78-225">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3a78-226">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="d3a78-226">Additional Resources</span></span>
* [<span data-ttu-id="d3a78-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3a78-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3a78-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3a78-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tangoe-tutorial/tutorial_general_205.png

























