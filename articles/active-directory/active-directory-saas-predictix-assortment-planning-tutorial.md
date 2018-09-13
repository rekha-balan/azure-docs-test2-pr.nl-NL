---
title: 'Tutorial: Azure Active Directory integration with Predictix Assortment Planning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Predictix Assortment Planning.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe5382d56aff1c495c7c473d72979187dd020557
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661834"
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="5aaaf-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="5aaaf-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>
<span data-ttu-id="5aaaf-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5aaaf-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5aaaf-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5aaaf-106">You can control in Azure AD who has access to Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="5aaaf-106">You can control in Azure AD who has access to Predictix Assortment Planning</span></span>
* <span data-ttu-id="5aaaf-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5aaaf-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="5aaaf-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="5aaaf-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5aaaf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5aaaf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aaaf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5aaaf-110">Prerequisites</span></span>
<span data-ttu-id="5aaaf-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span></span>

* <span data-ttu-id="5aaaf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5aaaf-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5aaaf-113">A Predictix Assortment Planning SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5aaaf-113">A Predictix Assortment Planning SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5aaaf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5aaaf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5aaaf-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5aaaf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5aaaf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5aaaf-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="5aaaf-118">Scenario Description</span></span>
<span data-ttu-id="5aaaf-119">In this tutorial, you test Microsoft Azure AD Single Sign-On in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-119">In this tutorial, you test Microsoft Azure AD Single Sign-On in a test environment.</span></span>

<span data-ttu-id="5aaaf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5aaaf-121">Adding Predictix Assortment Planning from the gallery</span><span class="sxs-lookup"><span data-stu-id="5aaaf-121">Adding Predictix Assortment Planning from the gallery</span></span>
2. <span data-ttu-id="5aaaf-122">Configuring and testing Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5aaaf-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-predictix-assortment-planning-from-the-gallery"></a><span data-ttu-id="5aaaf-123">Add Predictix Assortment Planning from the gallery</span><span class="sxs-lookup"><span data-stu-id="5aaaf-123">Add Predictix Assortment Planning from the gallery</span></span>
<span data-ttu-id="5aaaf-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5aaaf-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5aaaf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="5aaaf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5aaaf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="5aaaf-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="5aaaf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="5aaaf-135">In the search box, type **Predictix Assortment Planning**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-135">In the search box, type **Predictix Assortment Planning**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_01.png)
7. <span data-ttu-id="5aaaf-137">In the results pane, select **Predictix Assortment Planning**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-137">In the results pane, select **Predictix Assortment Planning**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_02.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="5aaaf-139">Configure and test Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5aaaf-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="5aaaf-140">In this section, you configure and test Microsoft Azure AD SSO with Predictix Assortment Planning based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5aaaf-140">In this section, you configure and test Microsoft Azure AD SSO with Predictix Assortment Planning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5aaaf-141">For SSO to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-141">For SSO to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span></span> <span data-ttu-id="5aaaf-142">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-142">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span></span>

<span data-ttu-id="5aaaf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Predictix Assortment Planning.</span></span>

<span data-ttu-id="5aaaf-144">To configure and test Microsoft Azure AD Single Sign-On with Predictix Assortment Planning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-144">To configure and test Microsoft Azure AD Single Sign-On with Predictix Assortment Planning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5aaaf-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5aaaf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="5aaaf-147">**[Creating a Predictix Assortment Planning test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-147">**[Creating a Predictix Assortment Planning test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5aaaf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="5aaaf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-microsoft-azure-ad-sso"></a><span data-ttu-id="5aaaf-150">Configure Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5aaaf-150">Configure Microsoft Azure AD SSO</span></span>
<span data-ttu-id="5aaaf-151">In this section, you enable Microsoft Azure AD Single Sign-On in the classic portal and configure single sign-on in your Predictix Assortment Planning application.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-151">In this section, you enable Microsoft Azure AD Single Sign-On in the classic portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="5aaaf-152">**To configure Microsoft Azure AD SSO with Predictix Assortment Planning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-152">**To configure Microsoft Azure AD SSO with Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="5aaaf-153">In the classic portal, on the **Predictix Assortment Planning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-153">In the classic portal, on the **Predictix Assortment Planning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="5aaaf-155">On the **How would you like users to sign on to Predictix Assortment Planning** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-155">On the **How would you like users to sign on to Predictix Assortment Planning** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_03.png) 
3. <span data-ttu-id="5aaaf-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_04.png) 
  1. <span data-ttu-id="5aaaf-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Predictix Assortment Planning application using the following pattern: **https://\<company name-pricing\>.ap.predictix.com/sso/request**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Predictix Assortment Planning application using the following pattern: **https://\<company name-pricing\>.ap.predictix.com/sso/request**.</span></span>
  2. <span data-ttu-id="5aaaf-160">click **Next**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-160">click **Next**</span></span>
4. <span data-ttu-id="5aaaf-161">On the **Configure single sign-on at Predictix Assortment Planning** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-161">On the **Configure single sign-on at Predictix Assortment Planning** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_05.png)
  1. <span data-ttu-id="5aaaf-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-163">Click **Download certificate**, and then save the file on your computer.</span></span>  
  2. <span data-ttu-id="5aaaf-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-164">Click **Next**.</span></span>
5. <span data-ttu-id="5aaaf-165">To get SSO configured for your application, contact Predictix Assortment Planning support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-165">To get SSO configured for your application, contact Predictix Assortment Planning support team and provide them with the following:</span></span>
   
  * <span data-ttu-id="5aaaf-166">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="5aaaf-166">The downloaded certificate</span></span>
  * <span data-ttu-id="5aaaf-167">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-167">The **Entity ID**</span></span>  
  * <span data-ttu-id="5aaaf-168">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-168">The **SAML SSO URL**</span></span>
  * <span data-ttu-id="5aaaf-169">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-169">The **Single Sign Out Service URL**</span></span>
6. <span data-ttu-id="5aaaf-170">In the classic portal, select the SSO configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-170">In the classic portal, select the SSO configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="5aaaf-172">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-172">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5aaaf-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5aaaf-174">Create an Azure AD test user</span></span>
<span data-ttu-id="5aaaf-175">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-175">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="5aaaf-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5aaaf-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="5aaaf-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5aaaf-181">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-181">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="5aaaf-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="5aaaf-185">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-185">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="5aaaf-187">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-187">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="5aaaf-188">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-188">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="5aaaf-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-189">Click **Next**.</span></span>
6. <span data-ttu-id="5aaaf-190">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-190">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="5aaaf-192">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-192">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="5aaaf-193">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-193">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="5aaaf-194">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-194">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="5aaaf-195">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-195">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="5aaaf-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-196">Click **Next**.</span></span>
7. <span data-ttu-id="5aaaf-197">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-197">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="5aaaf-199">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5aaaf-199">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="5aaaf-201">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-201">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="5aaaf-202">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-202">Click **Complete**.</span></span>   

### <a name="create-an-predictix-assortment-planning-test-user"></a><span data-ttu-id="5aaaf-203">Create an Predictix Assortment Planning test user</span><span class="sxs-lookup"><span data-stu-id="5aaaf-203">Create an Predictix Assortment Planning test user</span></span>
<span data-ttu-id="5aaaf-204">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-204">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="5aaaf-205">Please work with Predictix Assortment Planning support team to add the users in the Predictix Assortment Planning platform.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-205">Please work with Predictix Assortment Planning support team to add the users in the Predictix Assortment Planning platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5aaaf-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5aaaf-206">Assign the Azure AD test user</span></span>
<span data-ttu-id="5aaaf-207">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-207">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Predictix Assortment Planning.</span></span>

![Assign User][200] 

<span data-ttu-id="5aaaf-209">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5aaaf-209">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="5aaaf-210">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-210">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="5aaaf-212">In the applications list, select **Predictix Assortment Planning**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-212">In the applications list, select **Predictix Assortment Planning**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_50.png) 
3. <span data-ttu-id="5aaaf-214">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-214">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="5aaaf-216">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-216">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="5aaaf-217">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-217">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-sso"></a><span data-ttu-id="5aaaf-219">Test SSO</span><span class="sxs-lookup"><span data-stu-id="5aaaf-219">Test SSO</span></span>
<span data-ttu-id="5aaaf-220">In this section, you test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-220">In this section, you test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="5aaaf-221">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span><span class="sxs-lookup"><span data-stu-id="5aaaf-221">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5aaaf-222">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="5aaaf-222">Additional Resources</span></span>
* [<span data-ttu-id="5aaaf-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5aaaf-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5aaaf-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5aaaf-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_205.png

























