---
title: 'Tutorial: Azure Active Directory integration with Aravo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Aravo.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d86c0602b85dc24399446355f9b070c4b440b586
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563898"
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="005d8-103">Tutorial: Azure Active Directory integration with Aravo</span><span class="sxs-lookup"><span data-stu-id="005d8-103">Tutorial: Azure Active Directory integration with Aravo</span></span>
<span data-ttu-id="005d8-104">The objective of this tutorial is to show you how to integrate Aravo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="005d8-104">The objective of this tutorial is to show you how to integrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="005d8-105">Integrating Aravo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="005d8-105">Integrating Aravo with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="005d8-106">You can control in Azure AD who has access to Aravo</span><span class="sxs-lookup"><span data-stu-id="005d8-106">You can control in Azure AD who has access to Aravo</span></span>
* <span data-ttu-id="005d8-107">You can enable your users to automatically get signed-on to Aravo single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="005d8-107">You can enable your users to automatically get signed-on to Aravo single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="005d8-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="005d8-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="005d8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="005d8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="005d8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="005d8-110">Prerequisites</span></span>
<span data-ttu-id="005d8-111">To configure Azure AD integration with Aravo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="005d8-111">To configure Azure AD integration with Aravo, you need the following items:</span></span>

* <span data-ttu-id="005d8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="005d8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="005d8-113">A Aravo SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="005d8-113">A Aravo SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="005d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="005d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="005d8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="005d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="005d8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="005d8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="005d8-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="005d8-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="005d8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="005d8-118">Scenario description</span></span>
<span data-ttu-id="005d8-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="005d8-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="005d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="005d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="005d8-121">Adding Aravo from the gallery</span><span class="sxs-lookup"><span data-stu-id="005d8-121">Adding Aravo from the gallery</span></span>
2. <span data-ttu-id="005d8-122">Configuring and testing Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="005d8-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-aravo-from-the-gallery"></a><span data-ttu-id="005d8-123">Add Aravo from the gallery</span><span class="sxs-lookup"><span data-stu-id="005d8-123">Add Aravo from the gallery</span></span>
<span data-ttu-id="005d8-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="005d8-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="005d8-125">**To add Aravo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="005d8-125">**To add Aravo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="005d8-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005d8-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="005d8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="005d8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="005d8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="005d8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="005d8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="005d8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="005d8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="005d8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="005d8-135">In the search box, type **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="005d8-135">In the search box, type **Aravo**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_01.png)
7. <span data-ttu-id="005d8-137">In the results pane, select **Aravo**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="005d8-137">In the results pane, select **Aravo**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_0001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="005d8-139">Configure and test Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="005d8-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="005d8-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Aravo based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="005d8-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Aravo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="005d8-141">For SSO to work, Azure AD needs to know what the counterpart user in Aravo to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="005d8-141">For SSO to work, Azure AD needs to know what the counterpart user in Aravo to an user in Azure AD is.</span></span> <span data-ttu-id="005d8-142">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="005d8-142">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span></span>

<span data-ttu-id="005d8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Aravo.</span><span class="sxs-lookup"><span data-stu-id="005d8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Aravo.</span></span>

<span data-ttu-id="005d8-144">To configure and test Microsoft Azure AD SSO with Aravo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="005d8-144">To configure and test Microsoft Azure AD SSO with Aravo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="005d8-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="005d8-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="005d8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="005d8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="005d8-147">**[Creating a Aravo test user](#creating-a-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="005d8-147">**[Creating a Aravo test user](#creating-a-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="005d8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="005d8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="005d8-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="005d8-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-microsoft-azure-ad-sso"></a><span data-ttu-id="005d8-150">Configure Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="005d8-150">Configure Microsoft Azure AD SSO</span></span>
<span data-ttu-id="005d8-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your Aravo application.</span><span class="sxs-lookup"><span data-stu-id="005d8-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="005d8-152">**To configure Microsoft Azure AD SSO with Aravo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="005d8-152">**To configure Microsoft Azure AD SSO with Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="005d8-153">In the classic portal, on the **Aravo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="005d8-153">In the classic portal, on the **Aravo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="005d8-155">On the **How would you like users to sign on to Aravo** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-155">On the **How would you like users to sign on to Aravo** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_03.png) 
3. <span data-ttu-id="005d8-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="005d8-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_04.png)
  1. <span data-ttu-id="005d8-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="005d8-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.aravo.com`</span></span>
  2. <span data-ttu-id="005d8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="005d8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.aravo.com/aems/login.do`</span></span>
  3. <span data-ttu-id="005d8-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-161">Click **Next**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="005d8-162">Please note that these are not the real value.</span><span class="sxs-lookup"><span data-stu-id="005d8-162">Please note that these are not the real value.</span></span> <span data-ttu-id="005d8-163">You have to update the values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="005d8-163">You have to update the values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="005d8-164">To get these values, contact Aravo.</span><span class="sxs-lookup"><span data-stu-id="005d8-164">To get these values, contact Aravo.</span></span> 
    > 
4. <span data-ttu-id="005d8-165">On the **Configure single sign-on at Aravo** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="005d8-165">On the **Configure single sign-on at Aravo** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_05.png)
  1. <span data-ttu-id="005d8-167">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="005d8-167">Click **Download certificate**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="005d8-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-168">Click **Next**.</span></span>
5. <span data-ttu-id="005d8-169">To get SSO configured for your application, contact your Aravo support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="005d8-169">To get SSO configured for your application, contact your Aravo support team and provide them with the following:</span></span> 
 
  *  <span data-ttu-id="005d8-170">The **Downloaded certificate** file</span><span class="sxs-lookup"><span data-stu-id="005d8-170">The **Downloaded certificate** file</span></span>
  *  <span data-ttu-id="005d8-171">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="005d8-171">The **Issuer URL**</span></span> 
  *  <span data-ttu-id="005d8-172">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="005d8-172">The **SAML SSO URL**</span></span>
  *  <span data-ttu-id="005d8-173">The **single sign-out Service URL**</span><span class="sxs-lookup"><span data-stu-id="005d8-173">The **single sign-out Service URL**</span></span>
6. <span data-ttu-id="005d8-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="005d8-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="005d8-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="005d8-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="005d8-178">Create an Azure AD test user</span></span>
<span data-ttu-id="005d8-179">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="005d8-179">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="005d8-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="005d8-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="005d8-182">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="005d8-182">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="005d8-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="005d8-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="005d8-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="005d8-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="005d8-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="005d8-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="005d8-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="005d8-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="005d8-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="005d8-191">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="005d8-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="005d8-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="005d8-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-193">Click **Next**.</span></span>
6. <span data-ttu-id="005d8-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="005d8-194">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="005d8-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="005d8-196">In the **First Name** textbox, type **Britta**.</span></span> 
  2. <span data-ttu-id="005d8-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="005d8-197">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="005d8-198">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="005d8-198">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="005d8-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="005d8-199">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="005d8-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="005d8-200">Click **Next**.</span></span>
7. <span data-ttu-id="005d8-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="005d8-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="005d8-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="005d8-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="005d8-205">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="005d8-205">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="005d8-206">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="005d8-206">Click **Complete**.</span></span>   

### <a name="create-a-aravo-test-user"></a><span data-ttu-id="005d8-207">Create a Aravo test user</span><span class="sxs-lookup"><span data-stu-id="005d8-207">Create a Aravo test user</span></span>
<span data-ttu-id="005d8-208">The objective of this section is to create a user called Britta Simon in Aravo.Please work with Aravo support team to add the users in the Aravo account.</span><span class="sxs-lookup"><span data-stu-id="005d8-208">The objective of this section is to create a user called Britta Simon in Aravo.Please work with Aravo support team to add the users in the Aravo account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="005d8-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="005d8-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="005d8-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Aravo.</span><span class="sxs-lookup"><span data-stu-id="005d8-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Aravo.</span></span>

![Assign User][200]

<span data-ttu-id="005d8-212">**To assign Britta Simon to Aravo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="005d8-212">**To assign Britta Simon to Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="005d8-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="005d8-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="005d8-215">In the applications list, select **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="005d8-215">In the applications list, select **Aravo**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_50.png)
3. <span data-ttu-id="005d8-217">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="005d8-217">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="005d8-219">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="005d8-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="005d8-220">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="005d8-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="005d8-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="005d8-222">Test single sign-on</span></span>
<span data-ttu-id="005d8-223">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="005d8-223">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="005d8-224">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span><span class="sxs-lookup"><span data-stu-id="005d8-224">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="005d8-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="005d8-225">Additional resources</span></span>
* [<span data-ttu-id="005d8-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="005d8-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="005d8-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="005d8-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_205.png

























