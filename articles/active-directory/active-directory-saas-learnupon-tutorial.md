---
title: 'Tutorial: Azure Active Directory integration with Novatus | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LearnUpon.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: a595268b8b366fffb316875808c48f0f4e301fa3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556685"
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="a3819-103">Tutorial: Azure Active Directory integration with LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a3819-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>
<span data-ttu-id="a3819-104">The objective of this tutorial is to show you how to integrate LearnUpon with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3819-104">The objective of this tutorial is to show you how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3819-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a3819-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="a3819-106">You can control in Azure AD who has access to LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a3819-106">You can control in Azure AD who has access to LearnUpon</span></span>
* <span data-ttu-id="a3819-107">You can enable your users to automatically get signed-on to LearnUpon single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a3819-107">You can enable your users to automatically get signed-on to LearnUpon single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a3819-108">You can manage your accounts in one central location - the Azure Active Directory classic</span><span class="sxs-lookup"><span data-stu-id="a3819-108">You can manage your accounts in one central location - the Azure Active Directory classic</span></span> 

<span data-ttu-id="a3819-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3819-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3819-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3819-110">Prerequisites</span></span>
<span data-ttu-id="a3819-111">To configure Azure AD integration with LearnUpon, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a3819-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

* <span data-ttu-id="a3819-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a3819-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a3819-113">A LearnUpon single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a3819-113">A LearnUpon single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a3819-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a3819-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="a3819-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a3819-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a3819-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="a3819-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a3819-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3819-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3819-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="a3819-118">Scenario Description</span></span>
<span data-ttu-id="a3819-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a3819-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="a3819-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a3819-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3819-121">Adding LearnUpon from the gallery</span><span class="sxs-lookup"><span data-stu-id="a3819-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="a3819-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a3819-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="a3819-123">Adding LearnUpon from the gallery</span><span class="sxs-lookup"><span data-stu-id="a3819-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="a3819-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a3819-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3819-125">**To add LearnUpon from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3819-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3819-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3819-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a3819-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a3819-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a3819-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a3819-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="a3819-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a3819-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="a3819-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a3819-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="a3819-135">In the search box, type **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-135">In the search box, type **LearnUpon**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_01.png)
7. <span data-ttu-id="a3819-137">In the results pane, select **LearnUpon**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a3819-137">In the results pane, select **LearnUpon**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="a3819-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a3819-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="a3819-140">The objective of this section is to show you how to configure and test Azure AD SSO with LearnUpon based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a3819-140">The objective of this section is to show you how to configure and test Azure AD SSO with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3819-141">For SSO to work, Azure AD needs to know what the counterpart user in LearnUpon to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="a3819-141">For SSO to work, Azure AD needs to know what the counterpart user in LearnUpon to an user in Azure AD is.</span></span> <span data-ttu-id="a3819-142">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a3819-142">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>  

<span data-ttu-id="a3819-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a3819-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LearnUpon.</span></span>

<span data-ttu-id="a3819-144">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a3819-144">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3819-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a3819-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a3819-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3819-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3819-147">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="a3819-147">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a3819-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a3819-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3819-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a3819-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="a3819-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a3819-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="a3819-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your LearnUpon application.</span><span class="sxs-lookup"><span data-stu-id="a3819-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="a3819-152">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3819-152">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a3819-153">In the Azure classic portal, on the **LearnUpon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="a3819-153">In the Azure classic portal, on the **LearnUpon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="a3819-155">On the **How would you like users to sign on to LearnUpon** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-155">On the **How would you like users to sign on to LearnUpon** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_03.png) 
3. <span data-ttu-id="a3819-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="a3819-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_04.png) 
  1. <span data-ttu-id="a3819-159">In the **Reply URL** textbox, type the Assertion Consumer Service URL using the following pattern: `https://\<companyname\>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="a3819-159">In the **Reply URL** textbox, type the Assertion Consumer Service URL using the following pattern: `https://\<companyname\>.learnupon.com/saml/consumer`</span></span>
  2. <span data-ttu-id="a3819-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-160">Click **Next**.</span></span> 
4. <span data-ttu-id="a3819-161">On the **Configure single sign-on at LearnUpon** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-161">On the **Configure single sign-on at LearnUpon** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_05.png)   
  1. <span data-ttu-id="a3819-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a3819-163">Click **Download certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="a3819-164">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on LearnUpon side.</span><span class="sxs-lookup"><span data-stu-id="a3819-164">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on LearnUpon side.</span></span>
  2. <span data-ttu-id="a3819-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-165">Click **Next**.</span></span>
5. <span data-ttu-id="a3819-166">Open another browser instance and login into LearnUpon with an administrator account.</span><span class="sxs-lookup"><span data-stu-id="a3819-166">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 
6. <span data-ttu-id="a3819-167">Click the **settings** tab.</span><span class="sxs-lookup"><span data-stu-id="a3819-167">Click the **settings** tab.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png) 
7. <span data-ttu-id="a3819-169">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span><span class="sxs-lookup"><span data-stu-id="a3819-169">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 
8. <span data-ttu-id="a3819-171">In the **General Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-171">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  1. <span data-ttu-id="a3819-173">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="a3819-173">Select **Enabled**.</span></span>
  2. <span data-ttu-id="a3819-174">As **Version**, select **2.0**.</span><span class="sxs-lookup"><span data-stu-id="a3819-174">As **Version**, select **2.0**.</span></span>
  3. <span data-ttu-id="a3819-175">As **Skip conditions**, select **No**.</span><span class="sxs-lookup"><span data-stu-id="a3819-175">As **Skip conditions**, select **No**.</span></span>
  4. <span data-ttu-id="a3819-176">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="a3819-176">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>
  5. <span data-ttu-id="a3819-177">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a3819-177">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  6. <span data-ttu-id="a3819-178">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure classic portal login screen.</span><span class="sxs-lookup"><span data-stu-id="a3819-178">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure classic portal login screen.</span></span>
  <span data-ttu-id="a3819-179">7.in the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign out URL** textbos.</span><span class="sxs-lookup"><span data-stu-id="a3819-179">7.in the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign out URL** textbos.</span></span>
  8. <span data-ttu-id="a3819-180">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="a3819-180">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span> 
9. <span data-ttu-id="a3819-181">Click **User Settings**, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-181">Click **User Settings**, and then perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
  1. <span data-ttu-id="a3819-183">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname.</span><span class="sxs-lookup"><span data-stu-id="a3819-183">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname.</span></span> 
  2. <span data-ttu-id="a3819-184">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname.</span><span class="sxs-lookup"><span data-stu-id="a3819-184">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname.</span></span>
7. <span data-ttu-id="a3819-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-185">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="a3819-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a3819-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a3819-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a3819-189">Create an Azure AD test user</span></span>
<span data-ttu-id="a3819-190">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3819-190">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="a3819-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3819-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3819-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3819-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="a3819-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a3819-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a3819-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a3819-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="a3819-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="a3819-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="a3819-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="a3819-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="a3819-202">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="a3819-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-203">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="a3819-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-204">Click **Next**.</span></span>
6. <span data-ttu-id="a3819-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="a3819-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a3819-207">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="a3819-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-208">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="a3819-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="a3819-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="a3819-210">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="a3819-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3819-211">Click **Next**.</span></span>
7. <span data-ttu-id="a3819-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="a3819-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="a3819-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a3819-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="a3819-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="a3819-216">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="a3819-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a3819-217">Click **Complete**.</span></span>   

### <a name="create-a-learnupon-test-user"></a><span data-ttu-id="a3819-218">Create a LearnUpon test user</span><span class="sxs-lookup"><span data-stu-id="a3819-218">Create a LearnUpon test user</span></span>
<span data-ttu-id="a3819-219">The objective of this section is to create a user called Britta Simon in LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a3819-219">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="a3819-220">LearnUpon supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a3819-220">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a3819-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a3819-221">There is no action item for you in this section.</span></span> <span data-ttu-id="a3819-222">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a3819-222">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="a3819-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a3819-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="a3819-224">If you need to create an user manually, you need to contact the LearnUpon support team.</span><span class="sxs-lookup"><span data-stu-id="a3819-224">If you need to create an user manually, you need to contact the LearnUpon support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a3819-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a3819-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="a3819-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a3819-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to LearnUpon.</span></span>

![Assign User][200] 

<span data-ttu-id="a3819-228">**To assign Britta Simon to LearnUpon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a3819-228">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a3819-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a3819-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="a3819-231">In the applications list, select **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-231">In the applications list, select **LearnUpon**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_50.png) 
3. <span data-ttu-id="a3819-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a3819-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="a3819-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a3819-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a3819-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="a3819-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a3819-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a3819-238">Test single sign-on</span></span>
<span data-ttu-id="a3819-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a3819-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="a3819-240">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span><span class="sxs-lookup"><span data-stu-id="a3819-240">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3819-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="a3819-241">Additional Resources</span></span>
* [<span data-ttu-id="a3819-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3819-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3819-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3819-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learnupon-tutorial/tutorial_general_205.png





























