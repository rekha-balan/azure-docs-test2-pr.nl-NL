---
title: 'Tutorial: Azure Active Directory integration with Learning at Work | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Learning at Work.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: 8ed473852db131e6fa0c1f267bdbab2a7355a691
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661855"
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="2bc03-103">Tutorial: Azure Active Directory integration with Learning at Work</span><span class="sxs-lookup"><span data-stu-id="2bc03-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>
<span data-ttu-id="2bc03-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bc03-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bc03-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2bc03-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="2bc03-106">You can control in Azure AD who has access to Learning at Work</span><span class="sxs-lookup"><span data-stu-id="2bc03-106">You can control in Azure AD who has access to Learning at Work</span></span>
* <span data-ttu-id="2bc03-107">You can enable your users to automatically get signed-on to Learning at Work single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2bc03-107">You can enable your users to automatically get signed-on to Learning at Work single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="2bc03-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="2bc03-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="2bc03-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bc03-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bc03-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2bc03-110">Prerequisites</span></span>
<span data-ttu-id="2bc03-111">To configure Azure AD integration with Learning at Work, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2bc03-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

* <span data-ttu-id="2bc03-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2bc03-112">An Azure AD subscription</span></span>
* <span data-ttu-id="2bc03-113">A Learning at Work (Saba Cloud) single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2bc03-113">A Learning at Work (Saba Cloud) single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="2bc03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2bc03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="2bc03-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2bc03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2bc03-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="2bc03-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2bc03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bc03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bc03-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="2bc03-118">Scenario Description</span></span>
<span data-ttu-id="2bc03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2bc03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="2bc03-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2bc03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bc03-121">Adding Learning at Work from the gallery</span><span class="sxs-lookup"><span data-stu-id="2bc03-121">Adding Learning at Work from the gallery</span></span>
2. <span data-ttu-id="2bc03-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2bc03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-learning-at-work-from-the-gallery"></a><span data-ttu-id="2bc03-123">Add Learning at Work from the gallery</span><span class="sxs-lookup"><span data-stu-id="2bc03-123">Add Learning at Work from the gallery</span></span>
<span data-ttu-id="2bc03-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2bc03-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bc03-125">**To add Learning at Work from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2bc03-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc03-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="2bc03-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2bc03-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2bc03-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2bc03-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="2bc03-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2bc03-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="2bc03-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="2bc03-135">In the search box, type **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-135">In the search box, type **Learning at Work**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_01.png)
7. <span data-ttu-id="2bc03-137">In the results pane, select **Learning at Work**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="2bc03-137">In the results pane, select **Learning at Work**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2bc03-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2bc03-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2bc03-140">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2bc03-140">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bc03-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bc03-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="2bc03-142">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2bc03-142">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="2bc03-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="2bc03-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="2bc03-144">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2bc03-144">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bc03-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2bc03-145">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bc03-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bc03-146">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bc03-147">**[Create a Learning at Work test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="2bc03-147">**[Create a Learning at Work test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2bc03-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2bc03-148">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bc03-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2bc03-149">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2bc03-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2bc03-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="2bc03-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Learning at Work application.</span><span class="sxs-lookup"><span data-stu-id="2bc03-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="2bc03-152">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2bc03-152">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc03-153">In the classic portal, on the **Learning at Work** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="2bc03-153">In the classic portal, on the **Learning at Work** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="2bc03-155">On the **How would you like users to sign on to Learning at Work** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-155">On the **How would you like users to sign on to Learning at Work** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_03.png) 
3. <span data-ttu-id="2bc03-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2bc03-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_04.png) 
   
    1. <span data-ttu-id="2bc03-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Learning at Work application using the following pattern: `https://\<company name\>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="2bc03-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Learning at Work application using the following pattern: `https://\<company name\>.sabacloud.com/Saba/Web/<company code>`</span></span>
    2. <span data-ttu-id="2bc03-160">In the **Identifier** textbox, type the URL using the following pattern: `https://<company name>.sabacloud.com/Saba/SAML/sso/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="2bc03-160">In the **Identifier** textbox, type the URL using the following pattern: `https://<company name>.sabacloud.com/Saba/SAML/sso/alias/<company name>`</span></span>
    3. <span data-ttu-id="2bc03-161">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-161">click **Next**.</span></span>
4. <span data-ttu-id="2bc03-162">On the **Configure single sign-on at Learning at Work** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2bc03-162">On the **Configure single sign-on at Learning at Work** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_05.png)
   
    1. <span data-ttu-id="2bc03-164">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2bc03-164">Click **Download metadata**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="2bc03-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-165">Click **Next**.</span></span>
5. <span data-ttu-id="2bc03-166">To get SSO configured for your application, contact Learning at Work (Saba Cloud) support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="2bc03-166">To get SSO configured for your application, contact Learning at Work (Saba Cloud) support team and provide them with the following:</span></span>  
     * <span data-ttu-id="2bc03-167">The downloaded metadata</span><span class="sxs-lookup"><span data-stu-id="2bc03-167">The downloaded metadata</span></span>
     * <span data-ttu-id="2bc03-168">The **Issuer Url**</span><span class="sxs-lookup"><span data-stu-id="2bc03-168">The **Issuer Url**</span></span>
     * <span data-ttu-id="2bc03-169">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="2bc03-169">The **SAML SSO URL**</span></span>
     * <span data-ttu-id="2bc03-170">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="2bc03-170">The **Single Sign Out Service URL**</span></span>
6. <span data-ttu-id="2bc03-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="2bc03-173">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-173">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2bc03-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2bc03-175">Create an Azure AD test user</span></span>
<span data-ttu-id="2bc03-176">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bc03-176">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="2bc03-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2bc03-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc03-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="2bc03-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2bc03-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2bc03-182">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-182">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="2bc03-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="2bc03-186">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2bc03-186">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_05.png) 
  
    1. <span data-ttu-id="2bc03-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="2bc03-188">As Type Of User, select New user in your organization.</span></span>
    2. <span data-ttu-id="2bc03-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-189">In the User Name **textbox**, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="2bc03-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-190">Click **Next**.</span></span>
6. <span data-ttu-id="2bc03-191">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2bc03-191">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="2bc03-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-193">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="2bc03-194">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-194">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="2bc03-195">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="2bc03-196">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-196">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="2bc03-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-197">Click **Next**.</span></span>
7. <span data-ttu-id="2bc03-198">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-198">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="2bc03-200">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2bc03-200">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/create_aaduser_08.png) 
    1. <span data-ttu-id="2bc03-202">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-202">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="2bc03-203">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-203">Click **Complete**.</span></span>   

### <a name="create-an-learning-at-work-test-user"></a><span data-ttu-id="2bc03-204">Create an Learning at Work test user</span><span class="sxs-lookup"><span data-stu-id="2bc03-204">Create an Learning at Work test user</span></span>
<span data-ttu-id="2bc03-205">In this section, you create a user called Britta Simon in Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="2bc03-205">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="2bc03-206">Please work with Learning at Work support team to add the users in the Learning at Work platform.</span><span class="sxs-lookup"><span data-stu-id="2bc03-206">Please work with Learning at Work support team to add the users in the Learning at Work platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2bc03-207">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2bc03-207">Assign the Azure AD test user</span></span>
<span data-ttu-id="2bc03-208">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="2bc03-208">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Learning at Work.</span></span>

![Assign User][200] 

<span data-ttu-id="2bc03-210">**To assign Britta Simon to Learning at Work, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2bc03-210">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc03-211">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2bc03-211">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="2bc03-213">In the applications list, select **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-213">In the applications list, select **Learning at Work**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_50.png) 
3. <span data-ttu-id="2bc03-215">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-215">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="2bc03-217">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-217">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="2bc03-218">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="2bc03-218">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="2bc03-220">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2bc03-220">Test Single Sign-On</span></span>
<span data-ttu-id="2bc03-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2bc03-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2bc03-222">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span><span class="sxs-lookup"><span data-stu-id="2bc03-222">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bc03-223">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="2bc03-223">Additional Resources</span></span>
* [<span data-ttu-id="2bc03-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bc03-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bc03-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bc03-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-learning-at-work-tutorial/tutorial_general_205.png

























