---
title: 'Tutorial: Azure Active Directory integration with Nexonia | Microsoft Docs'
description: Learn how to use Nexonia with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: af9618c0-3437-4bb4-ad5a-568229b496db
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 003506b2daf2fc3e6364cb9bb6682d53226dcc36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554803"
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="e6dce-103">Tutorial: Azure Active Directory integration with Nexonia</span><span class="sxs-lookup"><span data-stu-id="e6dce-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="e6dce-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e6dce-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6dce-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e6dce-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e6dce-106">You can control in Azure AD who has access to Nexonia</span><span class="sxs-lookup"><span data-stu-id="e6dce-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="e6dce-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e6dce-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6dce-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e6dce-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e6dce-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e6dce-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6dce-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e6dce-110">Prerequisites</span></span>

<span data-ttu-id="e6dce-111">To configure Azure AD integration with Nexonia, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e6dce-111">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="e6dce-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e6dce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6dce-113">A Nexonia single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e6dce-113">A Nexonia single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="e6dce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e6dce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e6dce-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e6dce-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6dce-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e6dce-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e6dce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6dce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e6dce-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e6dce-118">Scenario description</span></span>
<span data-ttu-id="e6dce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e6dce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e6dce-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e6dce-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6dce-121">Adding Nexonia from the gallery</span><span class="sxs-lookup"><span data-stu-id="e6dce-121">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="e6dce-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e6dce-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="e6dce-123">Adding Nexonia from the gallery</span><span class="sxs-lookup"><span data-stu-id="e6dce-123">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="e6dce-124">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e6dce-124">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e6dce-125">**To add Nexonia from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e6dce-125">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e6dce-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="e6dce-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e6dce-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="e6dce-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e6dce-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="e6dce-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e6dce-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="e6dce-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="e6dce-135">In the search box, type **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-135">In the search box, type **Nexonia**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_01.png)

7. <span data-ttu-id="e6dce-137">In the results pane, select **Nexonia**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e6dce-137">In the results pane, select **Nexonia**, and then click **Complete** to add the application.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6dce-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e6dce-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6dce-140">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e6dce-140">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e6dce-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6dce-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="e6dce-142">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e6dce-142">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="e6dce-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nexonia.</span><span class="sxs-lookup"><span data-stu-id="e6dce-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nexonia.</span></span>

<span data-ttu-id="e6dce-144">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e6dce-144">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e6dce-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e6dce-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e6dce-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e6dce-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6dce-147">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e6dce-147">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e6dce-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e6dce-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6dce-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e6dce-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6dce-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e6dce-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6dce-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Nexonia application.</span><span class="sxs-lookup"><span data-stu-id="e6dce-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Nexonia application.</span></span>


<span data-ttu-id="e6dce-152">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e6dce-152">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="e6dce-153">In the classic portal, on the **Nexonia** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e6dce-153">In the classic portal, on the **Nexonia** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="e6dce-155">On the **How would you like users to sign on to Nexonia** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-155">On the **How would you like users to sign on to Nexonia** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_03.png) 

3. <span data-ttu-id="e6dce-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e6dce-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_04.png) 

    <span data-ttu-id="e6dce-159">a.</span><span class="sxs-lookup"><span data-stu-id="e6dce-159">a.</span></span> <span data-ttu-id="e6dce-160">In the **Reply URL** textbox, type the URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="e6dce-160">In the **Reply URL** textbox, type the URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>
    
    <span data-ttu-id="e6dce-161">b.</span><span class="sxs-lookup"><span data-stu-id="e6dce-161">b.</span></span> <span data-ttu-id="e6dce-162">click **Next**</span><span class="sxs-lookup"><span data-stu-id="e6dce-162">click **Next**</span></span>
 
4. <span data-ttu-id="e6dce-163">On the **Configure single sign-on at Nexonia** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e6dce-163">On the **Configure single sign-on at Nexonia** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_05.png)

    <span data-ttu-id="e6dce-165">a.</span><span class="sxs-lookup"><span data-stu-id="e6dce-165">a.</span></span> <span data-ttu-id="e6dce-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e6dce-166">Click **Download certificate**, and then save the file on your computer.</span></span>

    <span data-ttu-id="e6dce-167">b.</span><span class="sxs-lookup"><span data-stu-id="e6dce-167">b.</span></span> <span data-ttu-id="e6dce-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-168">Click **Next**.</span></span>


5. <span data-ttu-id="e6dce-169">To get SSO configured for your application, contact Nexonia support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="e6dce-169">To get SSO configured for your application, contact Nexonia support team and provide them with the following:</span></span>

    <span data-ttu-id="e6dce-170">• The downloaded **certificate**</span><span class="sxs-lookup"><span data-stu-id="e6dce-170">• The downloaded **certificate**</span></span>

    <span data-ttu-id="e6dce-171">• The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="e6dce-171">• The **Entity ID**</span></span>

    <span data-ttu-id="e6dce-172">• The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="e6dce-172">• The **SAML SSO URL**</span></span>

    <span data-ttu-id="e6dce-173">• The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="e6dce-173">• The **Single Sign Out Service URL**</span></span>

6. <span data-ttu-id="e6dce-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="e6dce-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6dce-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e6dce-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6dce-179">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e6dce-179">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Create Azure AD User][20]

<span data-ttu-id="e6dce-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e6dce-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e6dce-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="e6dce-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e6dce-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="e6dce-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6dce-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="e6dce-189">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="e6dce-189">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="e6dce-190">a.</span><span class="sxs-lookup"><span data-stu-id="e6dce-190">a.</span></span> <span data-ttu-id="e6dce-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e6dce-191">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="e6dce-192">b.</span><span class="sxs-lookup"><span data-stu-id="e6dce-192">b.</span></span> <span data-ttu-id="e6dce-193">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-193">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6dce-194">c.</span><span class="sxs-lookup"><span data-stu-id="e6dce-194">c.</span></span> <span data-ttu-id="e6dce-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-195">Click **Next**.</span></span>

6.  <span data-ttu-id="e6dce-196">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="e6dce-196">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="e6dce-197">a.</span><span class="sxs-lookup"><span data-stu-id="e6dce-197">a.</span></span> <span data-ttu-id="e6dce-198">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-198">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="e6dce-199">b.</span><span class="sxs-lookup"><span data-stu-id="e6dce-199">b.</span></span> <span data-ttu-id="e6dce-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-200">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="e6dce-201">c.</span><span class="sxs-lookup"><span data-stu-id="e6dce-201">c.</span></span> <span data-ttu-id="e6dce-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-202">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="e6dce-203">d.</span><span class="sxs-lookup"><span data-stu-id="e6dce-203">d.</span></span> <span data-ttu-id="e6dce-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-204">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="e6dce-205">e.</span><span class="sxs-lookup"><span data-stu-id="e6dce-205">e.</span></span> <span data-ttu-id="e6dce-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-206">Click **Next**.</span></span>

7. <span data-ttu-id="e6dce-207">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-207">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="e6dce-209">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e6dce-209">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="e6dce-211">a.</span><span class="sxs-lookup"><span data-stu-id="e6dce-211">a.</span></span> <span data-ttu-id="e6dce-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-212">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="e6dce-213">b.</span><span class="sxs-lookup"><span data-stu-id="e6dce-213">b.</span></span> <span data-ttu-id="e6dce-214">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-214">Click **Complete**.</span></span>   



### <a name="creating-an-nexonia-test-user"></a><span data-ttu-id="e6dce-215">Creating an Nexonia test user</span><span class="sxs-lookup"><span data-stu-id="e6dce-215">Creating an Nexonia test user</span></span>

<span data-ttu-id="e6dce-216">In this section, you create a user called Britta Simon in Nexonia.</span><span class="sxs-lookup"><span data-stu-id="e6dce-216">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="e6dce-217">Please work with Nexonia support team to add the users in the Nexonia platform.</span><span class="sxs-lookup"><span data-stu-id="e6dce-217">Please work with Nexonia support team to add the users in the Nexonia platform.</span></span> <span data-ttu-id="e6dce-218">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e6dce-218">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e6dce-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e6dce-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e6dce-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Nexonia.</span><span class="sxs-lookup"><span data-stu-id="e6dce-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Nexonia.</span></span>

![Assign User][200] 

<span data-ttu-id="e6dce-222">**To assign Britta Simon to Nexonia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e6dce-222">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="e6dce-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e6dce-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="e6dce-225">In the applications list, select **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-225">In the applications list, select **Nexonia**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_50.png) 

3. <span data-ttu-id="e6dce-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-227">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="e6dce-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-229">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="e6dce-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e6dce-230">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="e6dce-232">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e6dce-232">Testing Single Sign-On</span></span>

<span data-ttu-id="e6dce-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e6dce-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e6dce-234">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span><span class="sxs-lookup"><span data-stu-id="e6dce-234">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e6dce-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e6dce-235">Additional resources</span></span>

* [<span data-ttu-id="e6dce-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6dce-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6dce-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e6dce-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nexonia-tutorial/tutorial_general_205.png

























