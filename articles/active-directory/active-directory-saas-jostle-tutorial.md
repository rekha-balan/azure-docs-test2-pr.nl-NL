---
title: 'Tutorial: Azure Active Directory integration with Jostle | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jostle.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: c6327e9471731bbdefa45f37ecf221ed962951e9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550906"
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="3cdf9-103">Tutorial: Azure Active Directory integration with Jostle</span><span class="sxs-lookup"><span data-stu-id="3cdf9-103">Tutorial: Azure Active Directory integration with Jostle</span></span>
<span data-ttu-id="3cdf9-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cdf9-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cdf9-105">Integrating Jostle with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="3cdf9-106">You can control in Azure AD who has access to Jostle</span><span class="sxs-lookup"><span data-stu-id="3cdf9-106">You can control in Azure AD who has access to Jostle</span></span>
* <span data-ttu-id="3cdf9-107">You can enable your users to automatically get signed-on to Jostle single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3cdf9-107">You can enable your users to automatically get signed-on to Jostle single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="3cdf9-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="3cdf9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3cdf9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cdf9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cdf9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cdf9-110">Prerequisites</span></span>
<span data-ttu-id="3cdf9-111">To configure Azure AD integration with Jostle, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

* <span data-ttu-id="3cdf9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3cdf9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="3cdf9-113">A **Jostle** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3cdf9-113">A **Jostle** SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="3cdf9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="3cdf9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3cdf9-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3cdf9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cdf9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cdf9-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="3cdf9-118">Scenario Description</span></span>
<span data-ttu-id="3cdf9-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="3cdf9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cdf9-121">Adding Jostle from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cdf9-121">Adding Jostle from the gallery</span></span>
2. <span data-ttu-id="3cdf9-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3cdf9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="3cdf9-123">Adding Jostle from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cdf9-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="3cdf9-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cdf9-125">**To add Jostle from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cdf9-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cdf9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="3cdf9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3cdf9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="3cdf9-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="3cdf9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="3cdf9-135">In the search box, type **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-135">In the search box, type **Jostle**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_01.png)
7. <span data-ttu-id="3cdf9-137">In the results pane, select **Jostle**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-137">In the results pane, select **Jostle**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="3cdf9-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3cdf9-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="3cdf9-140">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3cdf9-140">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3cdf9-141">For SSO to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-141">For SSO to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="3cdf9-142">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-142">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="3cdf9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jostle.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jostle.</span></span>

<span data-ttu-id="3cdf9-144">To configure and test Azure AD SSO with Jostle, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-144">To configure and test Azure AD SSO with Jostle, you need to complete the following building blocks:</span></span>
1. <span data-ttu-id="3cdf9-145">**[Configuring Azure AD single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-145">**[Configuring Azure AD single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3cdf9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cdf9-147">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-147">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3cdf9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cdf9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="3cdf9-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3cdf9-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="3cdf9-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Jostle application.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Jostle application.</span></span>

<span data-ttu-id="3cdf9-152">**To configure Azure AD SSO with Jostle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cdf9-152">**To configure Azure AD SSO with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="3cdf9-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="3cdf9-155">In the classic portal, on the **Jostle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-155">In the classic portal, on the **Jostle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
3. <span data-ttu-id="3cdf9-157">On the **How would you like users to sign on to Jostle** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-157">On the **How would you like users to sign on to Jostle** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_06.png)
4. <span data-ttu-id="3cdf9-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_07.png)
  1. <span data-ttu-id="3cdf9-161">In the Sign On URL textbox, type a URL using the following pattern: `https://<subdomain>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="3cdf9-161">In the Sign On URL textbox, type a URL using the following pattern: `https://<subdomain>.jostle.us/jostle-prod/`</span></span>
  2. <span data-ttu-id="3cdf9-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-162">Click **Next**.</span></span>
5. <span data-ttu-id="3cdf9-163">On the **Configure single sign-on at Jostle** page, Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-163">On the **Configure single sign-on at Jostle** page, Click **Download metadata**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_08.png)
6. <span data-ttu-id="3cdf9-165">To get SSO configured for your application, contact your Jostle Account Manager or Jostle support.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-165">To get SSO configured for your application, contact your Jostle Account Manager or Jostle support.</span></span> <span data-ttu-id="3cdf9-166">They will assist with the proper channel to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-166">They will assist with the proper channel to configure SSO.</span></span> <span data-ttu-id="3cdf9-167">Please note that you have to send email and attach downloaded metadata file to <mailto:support@jostle.me>.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-167">Please note that you have to send email and attach downloaded metadata file to <mailto:support@jostle.me>.</span></span>
7. <span data-ttu-id="3cdf9-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="3cdf9-170">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3cdf9-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cdf9-172">Create an Azure AD test user</span></span>
<span data-ttu-id="3cdf9-173">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-173">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="3cdf9-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cdf9-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cdf9-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="3cdf9-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3cdf9-179">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-179">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="3cdf9-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="3cdf9-183">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-183">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="3cdf9-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-185">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="3cdf9-186">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="3cdf9-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-187">Click **Next**.</span></span>
6. <span data-ttu-id="3cdf9-188">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-188">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="3cdf9-190">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-190">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="3cdf9-191">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-191">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="3cdf9-192">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-192">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="3cdf9-193">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-193">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="3cdf9-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-194">Click **Next**.</span></span>
7. <span data-ttu-id="3cdf9-195">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-195">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="3cdf9-197">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cdf9-197">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="3cdf9-199">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-199">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="3cdf9-200">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-200">Click **Complete**.</span></span>   

### <a name="create-a-jostle-test-user"></a><span data-ttu-id="3cdf9-201">Create a Jostle test user</span><span class="sxs-lookup"><span data-stu-id="3cdf9-201">Create a Jostle test user</span></span>
<span data-ttu-id="3cdf9-202">In this section, you create a user called Britta Simon in Jostle.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-202">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="3cdf9-203">If you don't know how to add Britta Simon in Jostle, please work with Jostle support team to add the test user and enable SSO.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-203">If you don't know how to add Britta Simon in Jostle, please work with Jostle support team to add the test user and enable SSO.</span></span> <span data-ttu-id="3cdf9-204">Contact them at <mailto:support@jostle.me>.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-204">Contact them at <mailto:support@jostle.me>.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3cdf9-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cdf9-205">Assign the Azure AD test user</span></span>
<span data-ttu-id="3cdf9-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Jostle.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Jostle.</span></span>

![Assign User][200] 

<span data-ttu-id="3cdf9-208">**To assign Britta Simon to Jostle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cdf9-208">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="3cdf9-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="3cdf9-211">In the applications list, select **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-211">In the applications list, select **Jostle**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_jostle_50.png) 
3. <span data-ttu-id="3cdf9-213">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-213">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="3cdf9-215">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-215">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="3cdf9-216">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-216">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3cdf9-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cdf9-218">Test single sign-on</span></span>
<span data-ttu-id="3cdf9-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3cdf9-220">When you click the Jostle tile in the Access Panel, you should get automatically signed-on to your Jostle application.</span><span class="sxs-lookup"><span data-stu-id="3cdf9-220">When you click the Jostle tile in the Access Panel, you should get automatically signed-on to your Jostle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cdf9-221">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="3cdf9-221">Additional Resources</span></span>
* [<span data-ttu-id="3cdf9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cdf9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cdf9-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cdf9-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jostle-tutorial/tutorial_general_205.png



























