---
title: 'Tutorial: Azure Active Directory integration with Pantheon | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ede37f636104826b59240dc4660f1d8c4073aa58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662237"
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="c3095-103">Tutorial: Azure Active Directory integration with Pantheon</span><span class="sxs-lookup"><span data-stu-id="c3095-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="c3095-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3095-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3095-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c3095-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3095-106">You can control in Azure AD who has access to Pantheon</span><span class="sxs-lookup"><span data-stu-id="c3095-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="c3095-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c3095-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3095-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="c3095-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c3095-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3095-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3095-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3095-110">Prerequisites</span></span>

<span data-ttu-id="c3095-111">To configure Azure AD integration with Pantheon, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c3095-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="c3095-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c3095-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3095-113">A Pantheon single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c3095-113">A Pantheon single-sign on enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="c3095-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c3095-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c3095-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c3095-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3095-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c3095-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c3095-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3095-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c3095-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c3095-118">Scenario description</span></span>
<span data-ttu-id="c3095-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c3095-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="c3095-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3095-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3095-121">Adding Pantheon from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3095-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="c3095-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3095-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="c3095-123">Adding Pantheon from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3095-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="c3095-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c3095-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3095-125">**To add Pantheon from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3095-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3095-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3095-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="c3095-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c3095-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c3095-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c3095-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="c3095-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c3095-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="c3095-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c3095-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="c3095-135">In the search box, type **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-135">In the search box, type **Pantheon**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_01.png)

7. <span data-ttu-id="c3095-137">In the results pane, select **Pantheon**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c3095-137">In the results pane, select **Pantheon**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3095-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3095-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3095-140">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3095-140">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3095-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3095-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="c3095-142">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c3095-142">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="c3095-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="c3095-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pantheon.</span></span>

<span data-ttu-id="c3095-144">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3095-144">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3095-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c3095-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3095-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3095-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3095-147">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c3095-147">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c3095-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3095-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3095-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c3095-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3095-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3095-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3095-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Pantheon application.</span><span class="sxs-lookup"><span data-stu-id="c3095-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Pantheon application.</span></span>


<span data-ttu-id="c3095-152">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3095-152">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

<span data-ttu-id="c3095-153">Pantheon application expects the SAML assertion in specific format, which requires you to set the NameIdentifier attribute value with the user’s email address.</span><span class="sxs-lookup"><span data-stu-id="c3095-153">Pantheon application expects the SAML assertion in specific format, which requires you to set the NameIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="c3095-154">By default Azure AD uses the UserPrincipalName for NameIdentifier attribute.</span><span class="sxs-lookup"><span data-stu-id="c3095-154">By default Azure AD uses the UserPrincipalName for NameIdentifier attribute.</span></span> <span data-ttu-id="c3095-155">But for successful integration you need to adjust this value to match with user’s email address.</span><span class="sxs-lookup"><span data-stu-id="c3095-155">But for successful integration you need to adjust this value to match with user’s email address.</span></span>
<span data-ttu-id="c3095-156">The integration will only work after doing the correct mapping.</span><span class="sxs-lookup"><span data-stu-id="c3095-156">The integration will only work after doing the correct mapping.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_06.png)
    
1. <span data-ttu-id="c3095-158">In the classic portal, on the **Pantheon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c3095-158">In the classic portal, on the **Pantheon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="c3095-160">On the **How would you like users to sign on to Pantheon** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3095-160">On the **How would you like users to sign on to Pantheon** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_03.png) 

3. <span data-ttu-id="c3095-162">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3095-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_04.png) 

    <span data-ttu-id="c3095-164">a.</span><span class="sxs-lookup"><span data-stu-id="c3095-164">a.</span></span> <span data-ttu-id="c3095-165">In the **Identifier** textbox, type the URN using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="c3095-165">In the **Identifier** textbox, type the URN using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>
    
    <span data-ttu-id="c3095-166">b.</span><span class="sxs-lookup"><span data-stu-id="c3095-166">b.</span></span> <span data-ttu-id="c3095-167">In the **Reply URL** textbox, type the URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="c3095-167">In the **Reply URL** textbox, type the URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span> 

    <span data-ttu-id="c3095-168">c.</span><span class="sxs-lookup"><span data-stu-id="c3095-168">c.</span></span> <span data-ttu-id="c3095-169">click **Next**</span><span class="sxs-lookup"><span data-stu-id="c3095-169">click **Next**</span></span>
 
4. <span data-ttu-id="c3095-170">On the **Configure single sign-on at Pantheon** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3095-170">On the **Configure single sign-on at Pantheon** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_05.png)

    <span data-ttu-id="c3095-172">a.</span><span class="sxs-lookup"><span data-stu-id="c3095-172">a.</span></span> <span data-ttu-id="c3095-173">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c3095-173">Click **Download certificate**, and then save the file on your computer.</span></span>

    <span data-ttu-id="c3095-174">b.</span><span class="sxs-lookup"><span data-stu-id="c3095-174">b.</span></span> <span data-ttu-id="c3095-175">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3095-175">Click **Next**.</span></span>


5. <span data-ttu-id="c3095-176">To get SSO configured for your application, contact [Pantheon support](https://pantheon.io/docs/getting-support) team and provide them with the following information:</span><span class="sxs-lookup"><span data-stu-id="c3095-176">To get SSO configured for your application, contact [Pantheon support](https://pantheon.io/docs/getting-support) team and provide them with the following information:</span></span>

    <span data-ttu-id="c3095-177">• The downloaded **certificate**</span><span class="sxs-lookup"><span data-stu-id="c3095-177">• The downloaded **certificate**</span></span>

    <span data-ttu-id="c3095-178">• The **Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="c3095-178">• The **Single Sign-On Service URL**</span></span>

    >[!NOTE] 
    ><span data-ttu-id="c3095-179">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span><span class="sxs-lookup"><span data-stu-id="c3095-179">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="c3095-180">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="c3095-180">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

6. <span data-ttu-id="c3095-181">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3095-181">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="c3095-183">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c3095-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3095-185">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3095-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3095-186">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3095-186">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Create Azure AD User][20]

<span data-ttu-id="c3095-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3095-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3095-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3095-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="c3095-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c3095-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c3095-192">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c3095-192">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3095-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c3095-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="c3095-196">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="c3095-196">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="c3095-197">a.</span><span class="sxs-lookup"><span data-stu-id="c3095-197">a.</span></span> <span data-ttu-id="c3095-198">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c3095-198">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="c3095-199">b.</span><span class="sxs-lookup"><span data-stu-id="c3095-199">b.</span></span> <span data-ttu-id="c3095-200">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-200">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3095-201">c.</span><span class="sxs-lookup"><span data-stu-id="c3095-201">c.</span></span> <span data-ttu-id="c3095-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3095-202">Click **Next**.</span></span>

6.  <span data-ttu-id="c3095-203">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="c3095-203">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="c3095-204">a.</span><span class="sxs-lookup"><span data-stu-id="c3095-204">a.</span></span> <span data-ttu-id="c3095-205">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c3095-205">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="c3095-206">b.</span><span class="sxs-lookup"><span data-stu-id="c3095-206">b.</span></span> <span data-ttu-id="c3095-207">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-207">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="c3095-208">c.</span><span class="sxs-lookup"><span data-stu-id="c3095-208">c.</span></span> <span data-ttu-id="c3095-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c3095-210">d.</span><span class="sxs-lookup"><span data-stu-id="c3095-210">d.</span></span> <span data-ttu-id="c3095-211">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c3095-211">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="c3095-212">e.</span><span class="sxs-lookup"><span data-stu-id="c3095-212">e.</span></span> <span data-ttu-id="c3095-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c3095-213">Click **Next**.</span></span>

7. <span data-ttu-id="c3095-214">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c3095-214">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="c3095-216">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3095-216">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="c3095-218">a.</span><span class="sxs-lookup"><span data-stu-id="c3095-218">a.</span></span> <span data-ttu-id="c3095-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c3095-219">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="c3095-220">b.</span><span class="sxs-lookup"><span data-stu-id="c3095-220">b.</span></span> <span data-ttu-id="c3095-221">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c3095-221">Click **Complete**.</span></span>   



### <a name="creating-an-pantheon-test-user"></a><span data-ttu-id="c3095-222">Creating an Pantheon test user</span><span class="sxs-lookup"><span data-stu-id="c3095-222">Creating an Pantheon test user</span></span>

<span data-ttu-id="c3095-223">In this section, you create a user called Britta Simon in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="c3095-223">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="c3095-224">Please follow the below steps to add the user in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="c3095-224">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="c3095-225">For SSO to work user need to be created first in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="c3095-225">For SSO to work user need to be created first in Pantheon.</span></span>

1. <span data-ttu-id="c3095-226">Login to Pantheon with admin credentials.</span><span class="sxs-lookup"><span data-stu-id="c3095-226">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="c3095-227">Navigate to **Organization** dashboard page.</span><span class="sxs-lookup"><span data-stu-id="c3095-227">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="c3095-228">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="c3095-228">Click **People**.</span></span>

4. <span data-ttu-id="c3095-229">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="c3095-229">Click **Add user**.</span></span>

5. <span data-ttu-id="c3095-230">Enter the user's email address.</span><span class="sxs-lookup"><span data-stu-id="c3095-230">Enter the user's email address.</span></span>

6. <span data-ttu-id="c3095-231">Choose the user's role.</span><span class="sxs-lookup"><span data-stu-id="c3095-231">Choose the user's role.</span></span>

7. <span data-ttu-id="c3095-232">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="c3095-232">Click **Add user**.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3095-233">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3095-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3095-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pantheon.</span><span class="sxs-lookup"><span data-stu-id="c3095-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pantheon.</span></span>

![Assign User][200] 

<span data-ttu-id="c3095-236">**To assign Britta Simon to Pantheon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3095-236">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="c3095-237">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c3095-237">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="c3095-239">In the applications list, select **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-239">In the applications list, select **Pantheon**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_50.png) 

3. <span data-ttu-id="c3095-241">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c3095-241">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="c3095-243">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c3095-243">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="c3095-244">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c3095-244">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="c3095-246">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3095-246">Testing Single Sign-On</span></span>

<span data-ttu-id="c3095-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3095-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3095-248">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span><span class="sxs-lookup"><span data-stu-id="c3095-248">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c3095-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c3095-249">Additional resources</span></span>

* [<span data-ttu-id="c3095-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3095-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3095-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3095-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_205.png


























