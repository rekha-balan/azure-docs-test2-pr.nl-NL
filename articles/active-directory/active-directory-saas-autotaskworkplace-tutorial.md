---
title: 'Tutorial: Azure Active Directory integration with Autotask | Microsoft Docs'
description: Learn how to use Autotask with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 33b09e2b8fd4e3eaf030de7f34a61576908fb260
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662646"
---
# <a name="tutorial-azure-active-directory-integration-with-autotask"></a><span data-ttu-id="efdbb-103">Tutorial: Azure Active Directory integration with Autotask</span><span class="sxs-lookup"><span data-stu-id="efdbb-103">Tutorial: Azure Active Directory integration with Autotask</span></span>

<span data-ttu-id="efdbb-104">The objective of this tutorial is to show you how to integrate Autotask with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efdbb-104">The objective of this tutorial is to show you how to integrate Autotask with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efdbb-105">Integrating Autotask with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="efdbb-105">Integrating Autotask with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="efdbb-106">You can control in Azure AD who has access to Autotask</span><span class="sxs-lookup"><span data-stu-id="efdbb-106">You can control in Azure AD who has access to Autotask</span></span> 
- <span data-ttu-id="efdbb-107">You can enable your users to automatically get signed-on to Autotask (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="efdbb-107">You can enable your users to automatically get signed-on to Autotask (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efdbb-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="efdbb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="efdbb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efdbb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efdbb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="efdbb-110">Prerequisites</span></span>

<span data-ttu-id="efdbb-111">To configure Azure AD integration with Autotask, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="efdbb-111">To configure Azure AD integration with Autotask, you need the following items:</span></span>

- <span data-ttu-id="efdbb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="efdbb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efdbb-113">An Autotask single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="efdbb-113">An Autotask single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="efdbb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="efdbb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="efdbb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="efdbb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efdbb-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="efdbb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="efdbb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efdbb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="efdbb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="efdbb-118">Scenario description</span></span>
<span data-ttu-id="efdbb-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="efdbb-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="efdbb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="efdbb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efdbb-121">Adding Autotask from the gallery</span><span class="sxs-lookup"><span data-stu-id="efdbb-121">Adding Autotask from the gallery</span></span>
2. <span data-ttu-id="efdbb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="efdbb-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-autotask-from-the-gallery"></a><span data-ttu-id="efdbb-123">Adding Autotask from the gallery</span><span class="sxs-lookup"><span data-stu-id="efdbb-123">Adding Autotask from the gallery</span></span>
<span data-ttu-id="efdbb-124">To configure the integration of Autotask into Azure AD, you need to add Autotask from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="efdbb-124">To configure the integration of Autotask into Azure AD, you need to add Autotask from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efdbb-125">**To add Autotask from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="efdbb-125">**To add Autotask from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="efdbb-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efdbb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="efdbb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="efdbb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="efdbb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
    
    ![Applications][2]

4. <span data-ttu-id="efdbb-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="efdbb-131">Click **Add** at the bottom of the page.</span></span>
    
    ![Applications][3]

5. <span data-ttu-id="efdbb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="efdbb-135">In the search box, type **Autotask**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-135">In the search box, type **Autotask**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_01.png)

7. <span data-ttu-id="efdbb-137">In the results panel, select **Autotask**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="efdbb-137">In the results panel, select **Autotask**, and then click **Complete** to add the application.</span></span>

    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efdbb-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="efdbb-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efdbb-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Autotask based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="efdbb-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Autotask based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="efdbb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="efdbb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask to an user in Azure AD is.</span></span> <span data-ttu-id="efdbb-142">In other words, a link relationship between an Azure AD user and the related user in Autotask needs to be established.</span><span class="sxs-lookup"><span data-stu-id="efdbb-142">In other words, a link relationship between an Azure AD user and the related user in Autotask needs to be established.</span></span>

<span data-ttu-id="efdbb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Autotask.</span><span class="sxs-lookup"><span data-stu-id="efdbb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Autotask.</span></span> 

<span data-ttu-id="efdbb-144">To configure and test Azure AD single sign-on with Autotask, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="efdbb-144">To configure and test Azure AD single sign-on with Autotask, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="efdbb-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="efdbb-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="efdbb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efdbb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efdbb-147">**[Creating an Autotask test user](#creating-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="efdbb-147">**[Creating an Autotask test user](#creating-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="efdbb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="efdbb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efdbb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="efdbb-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efdbb-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="efdbb-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efdbb-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Autotask application.</span><span class="sxs-lookup"><span data-stu-id="efdbb-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Autotask application.</span></span>

<span data-ttu-id="efdbb-152">**To configure Azure AD single sign-on with Autotask, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="efdbb-152">**To configure Azure AD single sign-on with Autotask, perform the following steps:**</span></span>

1. <span data-ttu-id="efdbb-153">In the classic portal, on the **Autotask** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="efdbb-153">In the classic portal, on the **Autotask** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="efdbb-155">On the **How would you like users to sign on to Autotask** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-155">On the **How would you like users to sign on to Autotask** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_03.png)

3. <span data-ttu-id="efdbb-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="efdbb-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_04.png)

    <span data-ttu-id="efdbb-159">a.</span><span class="sxs-lookup"><span data-stu-id="efdbb-159">a.</span></span> <span data-ttu-id="efdbb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/singlesignon/saml/metadata`.</span><span class="sxs-lookup"><span data-stu-id="efdbb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/singlesignon/saml/metadata`.</span></span>

    <span data-ttu-id="efdbb-161">b.</span><span class="sxs-lookup"><span data-stu-id="efdbb-161">b.</span></span> <span data-ttu-id="efdbb-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="efdbb-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="efdbb-163">c.</span><span class="sxs-lookup"><span data-stu-id="efdbb-163">c.</span></span> <span data-ttu-id="efdbb-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-164">Click **Next**.</span></span>

4. <span data-ttu-id="efdbb-165">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-165">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_05.png)

    <span data-ttu-id="efdbb-167">a.</span><span class="sxs-lookup"><span data-stu-id="efdbb-167">a.</span></span> <span data-ttu-id="efdbb-168">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/loginsso`.</span><span class="sxs-lookup"><span data-stu-id="efdbb-168">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.awp.autotask.net/loginsso`.</span></span>

    <span data-ttu-id="efdbb-169">b.</span><span class="sxs-lookup"><span data-stu-id="efdbb-169">b.</span></span> <span data-ttu-id="efdbb-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-170">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="efdbb-171">Please note that you have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="efdbb-171">Please note that you have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="efdbb-172">To get these values, contact [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm).</span><span class="sxs-lookup"><span data-stu-id="efdbb-172">To get these values, contact [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm).</span></span>

4. <span data-ttu-id="efdbb-173">On the **Configure single sign-on at Autotask** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="efdbb-173">On the **Configure single sign-on at Autotask** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_06.png)

5. <span data-ttu-id="efdbb-175">To get SSO configured for your application, contact [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) and provide them with the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-175">To get SSO configured for your application, contact [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) and provide them with the downloaded **Metadata**.</span></span>

6. <span data-ttu-id="efdbb-176">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-176">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="efdbb-178">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-178">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efdbb-180">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="efdbb-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="efdbb-181">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efdbb-181">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="efdbb-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="efdbb-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="efdbb-184">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-184">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_09.png)

2. <span data-ttu-id="efdbb-186">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="efdbb-186">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="efdbb-187">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-187">To display the list of users, in the menu on the top, click **Users**.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="efdbb-189">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-189">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

5. <span data-ttu-id="efdbb-191">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="efdbb-191">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_05.png)

    <span data-ttu-id="efdbb-193">a.</span><span class="sxs-lookup"><span data-stu-id="efdbb-193">a.</span></span> <span data-ttu-id="efdbb-194">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="efdbb-194">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="efdbb-195">b.</span><span class="sxs-lookup"><span data-stu-id="efdbb-195">b.</span></span> <span data-ttu-id="efdbb-196">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-196">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efdbb-197">c.</span><span class="sxs-lookup"><span data-stu-id="efdbb-197">c.</span></span> <span data-ttu-id="efdbb-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-198">Click **Next**.</span></span>

6.  <span data-ttu-id="efdbb-199">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="efdbb-199">On the **User Profile** dialog page, perform the following steps:</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_06.png)

    <span data-ttu-id="efdbb-201">a.</span><span class="sxs-lookup"><span data-stu-id="efdbb-201">a.</span></span> <span data-ttu-id="efdbb-202">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-202">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="efdbb-203">b.</span><span class="sxs-lookup"><span data-stu-id="efdbb-203">b.</span></span> <span data-ttu-id="efdbb-204">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-204">In the **Last Name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="efdbb-205">c.</span><span class="sxs-lookup"><span data-stu-id="efdbb-205">c.</span></span> <span data-ttu-id="efdbb-206">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-206">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="efdbb-207">d.</span><span class="sxs-lookup"><span data-stu-id="efdbb-207">d.</span></span> <span data-ttu-id="efdbb-208">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-208">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="efdbb-209">e.</span><span class="sxs-lookup"><span data-stu-id="efdbb-209">e.</span></span> <span data-ttu-id="efdbb-210">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-210">Click **Next**.</span></span>

7. <span data-ttu-id="efdbb-211">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-211">On the **Get temporary password** dialog page, click **create**.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_07.png)

8. <span data-ttu-id="efdbb-213">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="efdbb-213">On the **Get temporary password** dialog page, perform the following steps:</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_08.png)

    <span data-ttu-id="efdbb-215">a.</span><span class="sxs-lookup"><span data-stu-id="efdbb-215">a.</span></span> <span data-ttu-id="efdbb-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-216">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="efdbb-217">b.</span><span class="sxs-lookup"><span data-stu-id="efdbb-217">b.</span></span> <span data-ttu-id="efdbb-218">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-218">Click **Complete**.</span></span>   



### <a name="creating-an-autotask-test-user"></a><span data-ttu-id="efdbb-219">Creating an Autotask test user</span><span class="sxs-lookup"><span data-stu-id="efdbb-219">Creating an Autotask test user</span></span>

<span data-ttu-id="efdbb-220">In this section, you create a user called Britta Simon in Autotask.</span><span class="sxs-lookup"><span data-stu-id="efdbb-220">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="efdbb-221">Please work with [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask platform.</span><span class="sxs-lookup"><span data-stu-id="efdbb-221">Please work with [Autotask support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="efdbb-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="efdbb-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="efdbb-223">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Autotask.</span><span class="sxs-lookup"><span data-stu-id="efdbb-223">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Autotask.</span></span>
    
![Assign User][200]

<span data-ttu-id="efdbb-225">**To assign Britta Simon to Autotask, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="efdbb-225">**To assign Britta Simon to Autotask, perform the following steps:**</span></span>

1. <span data-ttu-id="efdbb-226">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="efdbb-226">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
    
    ![Assign User][201]

2. <span data-ttu-id="efdbb-228">In the applications list, select **Autotask**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-228">In the applications list, select **Autotask**.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_50.png)

3. <span data-ttu-id="efdbb-230">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-230">In the menu on the top, click **Users**.</span></span>
    
    ![Assign User][203]

4. <span data-ttu-id="efdbb-232">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-232">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="efdbb-233">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="efdbb-233">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="efdbb-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="efdbb-235">Testing single sign-on</span></span>

<span data-ttu-id="efdbb-236">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="efdbb-236">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="efdbb-237">When you click the Autotask tile in the Access Panel, you should get automatically signed-on to your Autotask application.</span><span class="sxs-lookup"><span data-stu-id="efdbb-237">When you click the Autotask tile in the Access Panel, you should get automatically signed-on to your Autotask application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efdbb-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="efdbb-238">Additional resources</span></span>

* [<span data-ttu-id="efdbb-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efdbb-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efdbb-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efdbb-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_205.png


























