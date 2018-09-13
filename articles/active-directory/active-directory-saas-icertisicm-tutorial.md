---
title: 'Tutorial: Azure Active Directory integration with Icertis Contract Management Platform | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Icertis Contract Management Platform.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: b49c3487ba52e1d188c6a825517cf08fa9c87ab4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553738"
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="5c4bd-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="5c4bd-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>
<span data-ttu-id="5c4bd-104">The objective of this tutorial is to show you how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c4bd-104">The objective of this tutorial is to show you how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c4bd-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5c4bd-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="5c4bd-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span></span>
* <span data-ttu-id="5c4bd-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5c4bd-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="5c4bd-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="5c4bd-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5c4bd-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c4bd-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c4bd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5c4bd-110">Prerequisites</span></span>
<span data-ttu-id="5c4bd-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span></span>

* <span data-ttu-id="5c4bd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5c4bd-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5c4bd-113">A Icertis Contract Management Platform SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5c4bd-113">A Icertis Contract Management Platform SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5c4bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5c4bd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5c4bd-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5c4bd-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c4bd-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c4bd-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="5c4bd-118">Scenario Description</span></span>
<span data-ttu-id="5c4bd-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="5c4bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c4bd-121">Adding Icertis Contract Management Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="5c4bd-121">Adding Icertis Contract Management Platform from the gallery</span></span>
2. <span data-ttu-id="5c4bd-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5c4bd-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-icertis-contract-management-platform-from-the-gallery"></a><span data-ttu-id="5c4bd-123">Add Icertis Contract Management Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="5c4bd-123">Add Icertis Contract Management Platform from the gallery</span></span>
<span data-ttu-id="5c4bd-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c4bd-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c4bd-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="5c4bd-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5c4bd-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="5c4bd-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="5c4bd-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="5c4bd-135">In the search box, type **Icertis Contract Management Platform**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-135">In the search box, type **Icertis Contract Management Platform**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_01.png)
7. <span data-ttu-id="5c4bd-137">In the results pane, select **Icertis Contract Management Platform**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-137">In the results pane, select **Icertis Contract Management Platform**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="5c4bd-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5c4bd-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="5c4bd-140">The objective of this section is to show you how to configure and test Azure AD SSO with Icertis Contract Management Platform based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5c4bd-140">The objective of this section is to show you how to configure and test Azure AD SSO with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c4bd-141">For SSO to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-141">For SSO to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform to an user in Azure AD is.</span></span> <span data-ttu-id="5c4bd-142">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-142">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span></span>

<span data-ttu-id="5c4bd-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Icertis Contract Management Platform.</span></span>

<span data-ttu-id="5c4bd-144">To configure and test Azure AD SSO with Icertis Contract Management Platform, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-144">To configure and test Azure AD SSO with Icertis Contract Management Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c4bd-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c4bd-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c4bd-147">**[Creating a Icertis Contract Management Platform test user](#creating-a-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-147">**[Creating a Icertis Contract Management Platform test user](#creating-a-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5c4bd-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c4bd-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5c4bd-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c4bd-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="5c4bd-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Icertis Contract Management Platform application.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="5c4bd-152">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-152">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="5c4bd-153">In the classic portal, on the **Icertis Contract Management Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-153">In the classic portal, on the **Icertis Contract Management Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="5c4bd-155">On the **How would you like users to sign on to Icertis Contract Management Platform** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-155">On the **How would you like users to sign on to Icertis Contract Management Platform** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_03.png) 
3. <span data-ttu-id="5c4bd-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_04.png)
  1. <span data-ttu-id="5c4bd-159">In the **Sign On URL** textbox, type a URL using the following pattern:   `https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="5c4bd-159">In the **Sign On URL** textbox, type a URL using the following pattern:   `https://<company name>.icertis.com`</span></span>
  2. <span data-ttu-id="5c4bd-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-160">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5c4bd-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-161">Please note that these are not the real values.</span></span> <span data-ttu-id="5c4bd-162">You have to update these values with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-162">You have to update these values with the actual Sign On URL.</span></span> <span data-ttu-id="5c4bd-163">To get these values, contact Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-163">To get these values, contact Icertis Contract Management Platform.</span></span>
   >

1. <span data-ttu-id="5c4bd-164">On the **Configure single sign-on at Icertis Contract Management Platform** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-164">On the **Configure single sign-on at Icertis Contract Management Platform** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_05.png)
  1. <span data-ttu-id="5c4bd-166">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-166">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="5c4bd-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-167">Click **Next**.</span></span>
2. <span data-ttu-id="5c4bd-168">To get SSO configured for your application, contact your Icertis Contract Management Platform support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-168">To get SSO configured for your application, contact your Icertis Contract Management Platform support team and provide them with the following:</span></span> 
   *  <span data-ttu-id="5c4bd-169">The **downloaded metadata** file</span><span class="sxs-lookup"><span data-stu-id="5c4bd-169">The **downloaded metadata** file</span></span> 
   *  <span data-ttu-id="5c4bd-170">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-170">The **Entity ID**</span></span> 
   *  <span data-ttu-id="5c4bd-171">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-171">The **SAML SSO URL**</span></span> 
   *  <span data-ttu-id="5c4bd-172">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-172">The **Single Sign-Out Service URL**</span></span>
3. <span data-ttu-id="5c4bd-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="5c4bd-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5c4bd-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5c4bd-177">Create an Azure AD test user</span></span>
<span data-ttu-id="5c4bd-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="5c4bd-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c4bd-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="5c4bd-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5c4bd-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="5c4bd-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="5c4bd-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="5c4bd-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-190">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="5c4bd-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="5c4bd-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-192">Click **Next**.</span></span>
6. <span data-ttu-id="5c4bd-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="5c4bd-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="5c4bd-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="5c4bd-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="5c4bd-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="5c4bd-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-199">Click **Next**.</span></span>
7. <span data-ttu-id="5c4bd-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="5c4bd-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c4bd-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="5c4bd-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-204">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="5c4bd-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-205">Click **Complete**.</span></span>   

### <a name="create-a-icertis-contract-management-platform-test-user"></a><span data-ttu-id="5c4bd-206">Create a Icertis Contract Management Platform test user</span><span class="sxs-lookup"><span data-stu-id="5c4bd-206">Create a Icertis Contract Management Platform test user</span></span>
<span data-ttu-id="5c4bd-207">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-207">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="5c4bd-208">Please work with Icertis Contract Management Platform support team to add the users in the Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-208">Please work with Icertis Contract Management Platform support team to add the users in the Icertis Contract Management Platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5c4bd-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5c4bd-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="5c4bd-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Icertis Contract Management Platform.</span></span>

![Assign User][200]

<span data-ttu-id="5c4bd-212">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c4bd-212">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="5c4bd-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="5c4bd-215">In the applications list, select **Icertis Contract Management Platform**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-215">In the applications list, select **Icertis Contract Management Platform**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_50.png)
3. <span data-ttu-id="5c4bd-217">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-217">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="5c4bd-219">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="5c4bd-220">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="5c4bd-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c4bd-222">Test single sign-on</span></span>
<span data-ttu-id="5c4bd-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5c4bd-224">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span><span class="sxs-lookup"><span data-stu-id="5c4bd-224">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c4bd-225">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="5c4bd-225">Additional Resources</span></span>
* [<span data-ttu-id="5c4bd-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c4bd-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c4bd-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c4bd-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icertisicm-tutorial/tutorial_general_205.png

























