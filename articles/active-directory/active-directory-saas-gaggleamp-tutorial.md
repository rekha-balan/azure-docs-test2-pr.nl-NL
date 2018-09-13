---
title: 'Tutorial: Azure Active Directory integration with GaggleAMP | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GaggleAMP.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 582a8c3abd6acea2b16fe6b33187ccfa8bd53c4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661887"
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="d91ad-103">Tutorial: Azure Active Directory integration with GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="d91ad-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>
<span data-ttu-id="d91ad-104">The objective of this tutorial is to show you how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d91ad-104">The objective of this tutorial is to show you how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d91ad-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d91ad-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d91ad-106">You can control in Azure AD who has access to GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="d91ad-106">You can control in Azure AD who has access to GaggleAMP</span></span>
* <span data-ttu-id="d91ad-107">You can enable your users to automatically get signed-on to GaggleAMP single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d91ad-107">You can enable your users to automatically get signed-on to GaggleAMP single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d91ad-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d91ad-108">You can manage your accounts in one central location - the Azure classic portal</span></span> 

<span data-ttu-id="d91ad-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d91ad-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d91ad-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d91ad-110">Prerequisites</span></span>
<span data-ttu-id="d91ad-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d91ad-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

* <span data-ttu-id="d91ad-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d91ad-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d91ad-113">A GaggleAMP SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d91ad-113">A GaggleAMP SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d91ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d91ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="d91ad-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d91ad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d91ad-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d91ad-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d91ad-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d91ad-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d91ad-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d91ad-118">Scenario description</span></span>
<span data-ttu-id="d91ad-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d91ad-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="d91ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d91ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d91ad-121">Adding GaggleAMP from the gallery</span><span class="sxs-lookup"><span data-stu-id="d91ad-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="d91ad-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d91ad-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-gaggleamp-from-the-gallery"></a><span data-ttu-id="d91ad-123">Add GaggleAMP from the gallery</span><span class="sxs-lookup"><span data-stu-id="d91ad-123">Add GaggleAMP from the gallery</span></span>
<span data-ttu-id="d91ad-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d91ad-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d91ad-125">**To add GaggleAMP from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d91ad-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d91ad-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d91ad-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d91ad-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d91ad-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d91ad-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d91ad-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d91ad-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d91ad-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d91ad-135">In the search box, type **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-135">In the search box, type **GaggleAMP**.</span></span>
    <span data-ttu-id="d91ad-136">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_01.png)</span><span class="sxs-lookup"><span data-stu-id="d91ad-136">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_01.png)</span></span>
7. <span data-ttu-id="d91ad-137">In the results pane, select **GaggleAMP**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d91ad-137">In the results pane, select **GaggleAMP**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_02.png)>

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d91ad-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d91ad-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d91ad-140">The objective of this section is to show you how to configure and test Azure AD SSO with GaggleAMP based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d91ad-140">The objective of this section is to show you how to configure and test Azure AD SSO with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d91ad-141">For SSO to work, Azure AD needs to know the counterpart user in GaggleAMP to an user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d91ad-141">For SSO to work, Azure AD needs to know the counterpart user in GaggleAMP to an user in Azure AD.</span></span> <span data-ttu-id="d91ad-142">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d91ad-142">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="d91ad-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="d91ad-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GaggleAMP.</span></span>

<span data-ttu-id="d91ad-144">To configure and test Azure AD SSO with GaggleAMP, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d91ad-144">To configure and test Azure AD SSO with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d91ad-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d91ad-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d91ad-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d91ad-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d91ad-147">**[Creating a GaggleAMP test user](#creating-a-GaggleAMP-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d91ad-147">**[Creating a GaggleAMP test user](#creating-a-GaggleAMP-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d91ad-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d91ad-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d91ad-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d91ad-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="d91ad-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d91ad-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="d91ad-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your GaggleAMP application.</span><span class="sxs-lookup"><span data-stu-id="d91ad-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your GaggleAMP application.</span></span>

<span data-ttu-id="d91ad-152">**To configure Azure AD SSO with GaggleAMP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d91ad-152">**To configure Azure AD SSO with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="d91ad-153">In the Azure classic portal, on the **GaggleAMP** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d91ad-153">In the Azure classic portal, on the **GaggleAMP** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="d91ad-155">On the **How would you like users to sign on to GaggleAMP** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-155">On the **How would you like users to sign on to GaggleAMP** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_03.png) 
3. <span data-ttu-id="d91ad-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_04.png) 
   1. <span data-ttu-id="d91ad-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your GaggleAMP application using the following pattern: **“https://secure4.gaggleamp.com”**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your GaggleAMP application using the following pattern: **“https://secure4.gaggleamp.com”**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="d91ad-160">Please contact your [GaggleAMP sales team](mailto:sales@gaggleamp.com) if you need the **Sign On URL** for your application."</span><span class="sxs-lookup"><span data-stu-id="d91ad-160">Please contact your [GaggleAMP sales team](mailto:sales@gaggleamp.com) if you need the **Sign On URL** for your application."</span></span>
    >
   2. <span data-ttu-id="d91ad-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-161">Click **Next**.</span></span>

4. <span data-ttu-id="d91ad-162">On the **Configure single sign-on at GaggleAMP** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-162">On the **Configure single sign-on at GaggleAMP** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_05.png)   
  1. <span data-ttu-id="d91ad-164">Click **Download Certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d91ad-164">Click **Download Certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="d91ad-165">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on GaggleAMP side.</span><span class="sxs-lookup"><span data-stu-id="d91ad-165">We will need this certificate and Metadata URLs (Entity ID, SSO Sign In URL and Sign Out URL) to set up SSO on GaggleAMP side.</span></span>
  2. <span data-ttu-id="d91ad-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-166">Click **Next**.</span></span>
5. <span data-ttu-id="d91ad-167">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (e.g.: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="d91ad-167">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (e.g.: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>
6. <span data-ttu-id="d91ad-168">On your **SAML SSO** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-168">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png)  
  1. <span data-ttu-id="d91ad-170">On the Azure classic portal, copy the **Issuer URL**, and then paste it into the **Identity Provider Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="d91ad-170">On the Azure classic portal, copy the **Issuer URL**, and then paste it into the **Identity Provider Issuer** textbox.</span></span>  
  2. <span data-ttu-id="d91ad-171">On the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the **Identity Provider Single Sign-On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d91ad-171">On the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the **Identity Provider Single Sign-On URL** textbox.</span></span> 
  3. <span data-ttu-id="d91ad-172">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="d91ad-172">Click **Save**</span></span>      
  4. <span data-ttu-id="d91ad-173">Send the downloaded certificate to your [GaggleAMP sales team](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="d91ad-173">Send the downloaded certificate to your [GaggleAMP sales team](mailto:sales@gaggleamp.com).</span></span>
5. <span data-ttu-id="d91ad-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
6. <span data-ttu-id="d91ad-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d91ad-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d91ad-178">Create an Azure AD test user</span></span>
<span data-ttu-id="d91ad-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d91ad-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d91ad-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d91ad-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d91ad-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="d91ad-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d91ad-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d91ad-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d91ad-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="d91ad-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="d91ad-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d91ad-191">As Type Of User, select New user in your organization.</span></span>  
  2. <span data-ttu-id="d91ad-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d91ad-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-193">Click **Next**.</span></span>
6. <span data-ttu-id="d91ad-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-194">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="d91ad-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-196">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d91ad-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-197">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d91ad-198">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-198">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d91ad-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-199">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d91ad-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-200">Click **Next**.</span></span>
7. <span data-ttu-id="d91ad-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d91ad-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d91ad-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="d91ad-205">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-205">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="d91ad-206">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-206">Click **Complete**.</span></span>   

### <a name="create-a-gaggleamp-test-user"></a><span data-ttu-id="d91ad-207">Create a GaggleAMP test user</span><span class="sxs-lookup"><span data-stu-id="d91ad-207">Create a GaggleAMP test user</span></span>
<span data-ttu-id="d91ad-208">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="d91ad-208">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="d91ad-209">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="d91ad-209">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d91ad-210">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d91ad-210">There is no action item for you in this section.</span></span> <span data-ttu-id="d91ad-211">A new user will be created during an attempt to access GaggleAMP if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="d91ad-211">A new user will be created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d91ad-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d91ad-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="d91ad-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="d91ad-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to GaggleAMP.</span></span>

![Assign User][200] 

<span data-ttu-id="d91ad-215">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d91ad-215">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="d91ad-216">On the Azure portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d91ad-216">On the Azure portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="d91ad-218">In the applications list, select **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-218">In the applications list, select **GaggleAMP**.</span></span>
    <span data-ttu-id="d91ad-219">![Azure List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_50.png)</span><span class="sxs-lookup"><span data-stu-id="d91ad-219">![Azure List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_50.png)</span></span>
3. <span data-ttu-id="d91ad-220">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-220">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="d91ad-222">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d91ad-223">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d91ad-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d91ad-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d91ad-225">Test single sign-on</span></span>
<span data-ttu-id="d91ad-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d91ad-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d91ad-227">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span><span class="sxs-lookup"><span data-stu-id="d91ad-227">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d91ad-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d91ad-228">Additional resources</span></span>
* [<span data-ttu-id="d91ad-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d91ad-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d91ad-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d91ad-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-gaggleamp-tutorial/tutorial_general_205.png


























