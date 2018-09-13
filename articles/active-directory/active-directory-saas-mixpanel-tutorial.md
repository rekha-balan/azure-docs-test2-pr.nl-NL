---
title: 'Tutorial: Azure Active Directory integration with Mixpanel | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mixpanel.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: c1bdaa0ec259f2e8ac9a92d9423a082c18b1eed4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550094"
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="4dd08-103">Tutorial: Azure Active Directory integration with Mixpanel</span><span class="sxs-lookup"><span data-stu-id="4dd08-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>
<span data-ttu-id="4dd08-104">The objective of this tutorial is to show you how to integrate Mixpanel with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dd08-104">The objective of this tutorial is to show you how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dd08-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4dd08-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4dd08-106">You can control in Azure AD who has access to Mixpanel</span><span class="sxs-lookup"><span data-stu-id="4dd08-106">You can control in Azure AD who has access to Mixpanel</span></span>
* <span data-ttu-id="4dd08-107">You can enable your users to automatically get signed-on to Mixpanel single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4dd08-107">You can enable your users to automatically get signed-on to Mixpanel single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="4dd08-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4dd08-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4dd08-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4dd08-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dd08-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4dd08-110">Prerequisites</span></span>
<span data-ttu-id="4dd08-111">To configure Azure AD integration with Mixpanel, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4dd08-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

* <span data-ttu-id="4dd08-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4dd08-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4dd08-113">A Mixpanel single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4dd08-113">A Mixpanel single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="4dd08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4dd08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="4dd08-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4dd08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4dd08-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4dd08-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4dd08-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dd08-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dd08-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="4dd08-118">Scenario Description</span></span>
<span data-ttu-id="4dd08-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4dd08-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="4dd08-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dd08-121">Adding Mixpanel from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd08-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="4dd08-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="4dd08-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-mixpanel-from-the-gallery"></a><span data-ttu-id="4dd08-123">Add Mixpanel from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dd08-123">Add Mixpanel from the gallery</span></span>
<span data-ttu-id="4dd08-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4dd08-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dd08-125">**To add Mixpanel from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd08-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd08-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="4dd08-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4dd08-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4dd08-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4dd08-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="4dd08-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4dd08-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="4dd08-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="4dd08-135">In the search box, type **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-135">In the search box, type **Mixpanel**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_01.png)
7. <span data-ttu-id="4dd08-137">In the results pane, select **Mixpanel**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4dd08-137">In the results pane, select **Mixpanel**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="4dd08-138">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="4dd08-138">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="4dd08-139">The objective of this section is to show you how to configure and test Azure AD SSO with Mixpanel based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4dd08-139">The objective of this section is to show you how to configure and test Azure AD SSO with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4dd08-140">For SSO to work, Azure AD needs to know what the counterpart user in Mixpanel to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="4dd08-140">For SSO to work, Azure AD needs to know what the counterpart user in Mixpanel to an user in Azure AD is.</span></span> <span data-ttu-id="4dd08-141">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4dd08-141">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="4dd08-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="4dd08-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Mixpanel.</span></span>

<span data-ttu-id="4dd08-143">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dd08-143">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dd08-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4dd08-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4dd08-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd08-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4dd08-146">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="4dd08-146">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4dd08-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dd08-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4dd08-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4dd08-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4dd08-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd08-149">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="4dd08-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Mixpanel application.</span><span class="sxs-lookup"><span data-stu-id="4dd08-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Mixpanel application.</span></span>

<span data-ttu-id="4dd08-151">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd08-151">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd08-152">In the Azure classic portal, on the **Mixpanel** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="4dd08-152">In the Azure classic portal, on the **Mixpanel** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="4dd08-154">On the **How would you like users to sign on to Mixpanel** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-154">On the **How would you like users to sign on to Mixpanel** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_03.png) 
3. <span data-ttu-id="4dd08-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd08-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_04.png)
  1. <span data-ttu-id="4dd08-158">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Mixpanel application using the following pattern: **“https://mixpanel.com/login/”**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-158">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Mixpanel application using the following pattern: **“https://mixpanel.com/login/”**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4dd08-159">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@Mixpanel.com) to enable SSO settings for you tenant.</span><span class="sxs-lookup"><span data-stu-id="4dd08-159">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@Mixpanel.com) to enable SSO settings for you tenant.</span></span> <span data-ttu-id="4dd08-160">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span><span class="sxs-lookup"><span data-stu-id="4dd08-160">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span>
    >

  2. <span data-ttu-id="4dd08-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-161">Click **Next**.</span></span>

1. <span data-ttu-id="4dd08-162">On the **Configure single sign-on at Mixpanel** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd08-162">On the **Configure single sign-on at Mixpanel** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_05.png) 
  1. <span data-ttu-id="4dd08-164">Click **Download Certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4dd08-164">Click **Download Certificate**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="4dd08-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-165">Click **Next**.</span></span>
2. <span data-ttu-id="4dd08-166">In a different browser window, sign-on to your Mixpanel application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4dd08-166">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>
3. <span data-ttu-id="4dd08-167">On bottom of the page, click the little **gear** icon in the left corner.</span><span class="sxs-lookup"><span data-stu-id="4dd08-167">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 
4. <span data-ttu-id="4dd08-169">Click the **Access security** tab, and then click **Change settings**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-169">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 
5. <span data-ttu-id="4dd08-171">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-171">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **Next**.</span></span>
   
    ![Mixpanel Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 
6. <span data-ttu-id="4dd08-173">In the Azure classic portal, on the **Configure single sign-on at Mixpanel** dialog page, copy the **Single Sign-On Service URL** value, paste it into the authentication URL textbox on the **Change your authentication  URL** dialog page, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-173">In the Azure classic portal, on the **Configure single sign-on at Mixpanel** dialog page, copy the **Single Sign-On Service URL** value, paste it into the authentication URL textbox on the **Change your authentication  URL** dialog page, and then click **Next**.</span></span>
   
    ![Mixpanel Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 
7. <span data-ttu-id="4dd08-175">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-175">Click **Done**.</span></span>
8. <span data-ttu-id="4dd08-176">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-176">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="4dd08-178">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-178">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4dd08-180">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd08-180">Create an Azure AD test user</span></span>
<span data-ttu-id="4dd08-181">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd08-181">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

* <span data-ttu-id="4dd08-182">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-182">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="4dd08-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd08-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd08-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-185">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="4dd08-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4dd08-187">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4dd08-188">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-188">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="4dd08-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-190">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="4dd08-192">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd08-192">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="4dd08-194">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="4dd08-194">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="4dd08-195">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-195">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="4dd08-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-196">Click **Next**.</span></span>
6. <span data-ttu-id="4dd08-197">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd08-197">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="4dd08-199">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-199">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="4dd08-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-200">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="4dd08-201">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-201">In the **Display Name** textbox, type **Britta Simon**.</span></span>  
 4. <span data-ttu-id="4dd08-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-202">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="4dd08-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-203">Click **Next**.</span></span>
7. <span data-ttu-id="4dd08-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="4dd08-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dd08-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="4dd08-208">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-208">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="4dd08-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-209">Click **Complete**.</span></span>   

### <a name="create-a-mixpanel-test-user"></a><span data-ttu-id="4dd08-210">Create a Mixpanel test user</span><span class="sxs-lookup"><span data-stu-id="4dd08-210">Create a Mixpanel test user</span></span>
<span data-ttu-id="4dd08-211">The objective of this section is to create a user called Britta Simon in Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="4dd08-211">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="4dd08-212">Sign-on to your Mixpanel company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4dd08-212">Sign-on to your Mixpanel company site as an administrator.</span></span>
2. <span data-ttu-id="4dd08-213">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span><span class="sxs-lookup"><span data-stu-id="4dd08-213">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>
3. <span data-ttu-id="4dd08-214">Click the **Team** tab.</span><span class="sxs-lookup"><span data-stu-id="4dd08-214">Click the **Team** tab.</span></span>
4. <span data-ttu-id="4dd08-215">In the **team member** textbox, type Britta's email address in the Azure.</span><span class="sxs-lookup"><span data-stu-id="4dd08-215">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Mixpanel Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 
5. <span data-ttu-id="4dd08-217">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-217">Click **Invite**.</span></span> 

<span data-ttu-id="4dd08-218">The user will get an email to set his profile up.</span><span class="sxs-lookup"><span data-stu-id="4dd08-218">The user will get an email to set his profile up.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4dd08-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dd08-219">Assign the Azure AD test user</span></span>
<span data-ttu-id="4dd08-220">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="4dd08-220">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Mixpanel.</span></span>

![Assign User][200] 

<span data-ttu-id="4dd08-222">**To assign Britta Simon to Mixpanel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dd08-222">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="4dd08-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4dd08-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="4dd08-225">In the applications list, select **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-225">In the applications list, select **Mixpanel**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_50.png) 
3. <span data-ttu-id="4dd08-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-227">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="4dd08-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-229">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="4dd08-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="4dd08-230">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4dd08-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dd08-232">Test single sign-on</span></span>
<span data-ttu-id="4dd08-233">The objective of this section is to test your Azure AD single SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4dd08-233">The objective of this section is to test your Azure AD single SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4dd08-234">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span><span class="sxs-lookup"><span data-stu-id="4dd08-234">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4dd08-235">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="4dd08-235">Additional Resources</span></span>
* [<span data-ttu-id="4dd08-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dd08-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4dd08-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dd08-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mixpanel-tutorial/tutorial_general_205.png





























