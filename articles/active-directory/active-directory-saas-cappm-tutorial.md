---
title: 'Tutorial: Azure Active Directory integration with CA PPM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CA PPM.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: e8542c8480a746449bbdfe7aa3bc6fc794b00f93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563126"
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="4fc1c-103">Tutorial: Azure Active Directory integration with CA PPM</span><span class="sxs-lookup"><span data-stu-id="4fc1c-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>
<span data-ttu-id="4fc1c-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fc1c-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fc1c-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4fc1c-106">You can control in Azure AD who has access to CA PPM</span><span class="sxs-lookup"><span data-stu-id="4fc1c-106">You can control in Azure AD who has access to CA PPM</span></span>
* <span data-ttu-id="4fc1c-107">You can enable your users to automatically get signed-on to CA PPM single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4fc1c-107">You can enable your users to automatically get signed-on to CA PPM single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="4fc1c-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4fc1c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4fc1c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fc1c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc1c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4fc1c-110">Prerequisites</span></span>
<span data-ttu-id="4fc1c-111">To configure Azure AD integration with CA PPM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-111">To configure Azure AD integration with CA PPM, you need the following items:</span></span>

* <span data-ttu-id="4fc1c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4fc1c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4fc1c-113">A CA PPM single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4fc1c-113">A CA PPM single-sign on (SSO) enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fc1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="4fc1c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4fc1c-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4fc1c-117">If you don't have an Azure AD trial environment, you can get [a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fc1c-117">If you don't have an Azure AD trial environment, you can get [a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fc1c-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="4fc1c-118">Scenario Description</span></span>
<span data-ttu-id="4fc1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="4fc1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fc1c-121">Adding CA PPM from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fc1c-121">Adding CA PPM from the gallery</span></span>
2. <span data-ttu-id="4fc1c-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="4fc1c-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-ca-ppm-from-the-gallery"></a><span data-ttu-id="4fc1c-123">Adding CA PPM from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fc1c-123">Adding CA PPM from the gallery</span></span>
<span data-ttu-id="4fc1c-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fc1c-125">**To add CA PPM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-125">**To add CA PPM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc1c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="4fc1c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4fc1c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="4fc1c-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="4fc1c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="4fc1c-135">In the search box, type **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-135">In the search box, type **CA PPM**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_01.png)
7. <span data-ttu-id="4fc1c-137">In the results pane, select **CA PPM**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-137">In the results pane, select **CA PPM**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="4fc1c-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="4fc1c-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="4fc1c-140">In this section, you configure and test Azure AD SSO with CA PPM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4fc1c-140">In this section, you configure and test Azure AD SSO with CA PPM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fc1c-141">For SSO to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-141">For SSO to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span></span> <span data-ttu-id="4fc1c-142">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-142">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span></span>

<span data-ttu-id="4fc1c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CA PPM.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in CA PPM.</span></span>

<span data-ttu-id="4fc1c-144">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-144">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4fc1c-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4fc1c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fc1c-147">**[Creating a CA PPM test user](#creating-an-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-147">**[Creating a CA PPM test user](#creating-an-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4fc1c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fc1c-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4fc1c-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc1c-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="4fc1c-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your CA PPM application.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your CA PPM application.</span></span>

<span data-ttu-id="4fc1c-152">**To configure Azure AD SSO with CA PPM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-152">**To configure Azure AD SSO with CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc1c-153">In the classic portal, on the **CA PPM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-153">In the classic portal, on the **CA PPM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="4fc1c-155">On the **How would you like users to sign on to CA PPM** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-155">On the **How would you like users to sign on to CA PPM** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_03.png) 
3. <span data-ttu-id="4fc1c-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_04.png) 
  1. <span data-ttu-id="4fc1c-159">In the **Identifier** textbox, type the URL used by your users to sign-on to your CA PPM application using the following pattern: **https://ca.ondemand.saml.20.post.\<company name\>**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-159">In the **Identifier** textbox, type the URL used by your users to sign-on to your CA PPM application using the following pattern: **https://ca.ondemand.saml.20.post.\<company name\>**.</span></span>
  2. <span data-ttu-id="4fc1c-160">In the **Reply URL** textbox type **https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-160">In the **Reply URL** textbox type **https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer**</span></span> 
  3. <span data-ttu-id="4fc1c-161">click **Next**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-161">click **Next**</span></span>
4. <span data-ttu-id="4fc1c-162">On the **Configure single sign-on at CA PPM** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-162">On the **Configure single sign-on at CA PPM** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_05.png)
  1. <span data-ttu-id="4fc1c-164">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-164">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="4fc1c-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-165">Click **Next**.</span></span>
5. <span data-ttu-id="4fc1c-166">To get SSO configured for your application, contact [CA Technical Support](mailto:catechnicalsupport@ca.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-166">To get SSO configured for your application, contact [CA Technical Support](mailto:catechnicalsupport@ca.com) and provide them with the following:</span></span>
  
  * <span data-ttu-id="4fc1c-167">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="4fc1c-167">The downloaded certificate</span></span>
  * <span data-ttu-id="4fc1c-168">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-168">The **Entity ID**</span></span>
6. <span data-ttu-id="4fc1c-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="4fc1c-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fc1c-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fc1c-173">Create an Azure AD test user</span></span>
<span data-ttu-id="4fc1c-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="4fc1c-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc1c-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="4fc1c-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4fc1c-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="4fc1c-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="4fc1c-184">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="4fc1c-184">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_05.png)</span></span> 
  1. <span data-ttu-id="4fc1c-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-185">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="4fc1c-186">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="4fc1c-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-187">Click **Next**.</span></span>
6. <span data-ttu-id="4fc1c-188">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-188">On the **User Profile** dialog page, perform the following steps:</span></span>

 ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_06.png)   
  1. <span data-ttu-id="4fc1c-190">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-190">In the **First Name** textbox, type **Britta**.</span></span>    
  2. <span data-ttu-id="4fc1c-191">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-191">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="4fc1c-192">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-192">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="4fc1c-193">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-193">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="4fc1c-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-194">Click **Next**.</span></span>
7. <span data-ttu-id="4fc1c-195">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-195">On the **Get temporary password** dialog page, click **create**.</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="4fc1c-197">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc1c-197">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/create_aaduser_08.png)  
  1. <span data-ttu-id="4fc1c-199">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-199">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="4fc1c-200">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-200">Click **Complete**.</span></span>   

### <a name="create-an-ca-ppm-test-user"></a><span data-ttu-id="4fc1c-201">Create an CA PPM test user</span><span class="sxs-lookup"><span data-stu-id="4fc1c-201">Create an CA PPM test user</span></span>
<span data-ttu-id="4fc1c-202">In this section, you create a user called Britta Simon in CA PPM.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-202">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="4fc1c-203">Please work with CA PPM support team to add the users in the CA PPM platform.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-203">Please work with CA PPM support team to add the users in the CA PPM platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4fc1c-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fc1c-204">Assign the Azure AD test user</span></span>
<span data-ttu-id="4fc1c-205">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to CA PPM.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-205">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to CA PPM.</span></span>

![Assign User][200] 

<span data-ttu-id="4fc1c-207">**To assign Britta Simon to CA PPM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc1c-207">**To assign Britta Simon to CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc1c-208">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-208">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="4fc1c-210">In the applications list, select **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-210">In the applications list, select **CA PPM**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_cappm_50.png) 
3. <span data-ttu-id="4fc1c-212">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-212">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="4fc1c-214">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-214">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="4fc1c-215">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-215">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4fc1c-217">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc1c-217">Test single sign-on</span></span>
<span data-ttu-id="4fc1c-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4fc1c-219">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span><span class="sxs-lookup"><span data-stu-id="4fc1c-219">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fc1c-220">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="4fc1c-220">Additional Resources</span></span>
* [<span data-ttu-id="4fc1c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fc1c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fc1c-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fc1c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cappm-tutorial/tutorial_general_205.png

























