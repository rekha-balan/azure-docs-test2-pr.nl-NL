---
title: 'Tutorial: Azure Active Directory integration with Wizergos Productivity Software  | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Wizergos Productivity Software.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a9b1a59f0e1bb3e8f4a17c77f4aa6b145295b35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669946"
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="8320a-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="8320a-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="8320a-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8320a-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8320a-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8320a-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8320a-106">You can control in Azure AD who has access to Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="8320a-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="8320a-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8320a-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="8320a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8320a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8320a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8320a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8320a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8320a-110">Prerequisites</span></span>
<span data-ttu-id="8320a-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8320a-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="8320a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8320a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8320a-113">A Wizergos Productivity Software SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8320a-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="8320a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8320a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="8320a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8320a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8320a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8320a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8320a-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8320a-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8320a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8320a-118">Scenario description</span></span>
<span data-ttu-id="8320a-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8320a-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="8320a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8320a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8320a-121">Adding Wizergos Productivity Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="8320a-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="8320a-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8320a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="8320a-123">Adding Wizergos Productivity Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="8320a-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="8320a-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8320a-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8320a-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8320a-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8320a-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8320a-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="8320a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8320a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8320a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8320a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="8320a-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8320a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="8320a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8320a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="8320a-135">In the search box, type **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="8320a-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="8320a-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8320a-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="8320a-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8320a-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="8320a-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8320a-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8320a-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="8320a-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="8320a-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8320a-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="8320a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="8320a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="8320a-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8320a-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8320a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8320a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8320a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8320a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8320a-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8320a-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8320a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8320a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8320a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8320a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="8320a-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8320a-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="8320a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span><span class="sxs-lookup"><span data-stu-id="8320a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="8320a-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8320a-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8320a-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="8320a-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="8320a-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="8320a-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="8320a-157">On the **Configure App Settings** dialog page, click **Next**:</span><span class="sxs-lookup"><span data-stu-id="8320a-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="8320a-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="8320a-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="8320a-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8320a-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="8320a-162">From the hamburger menu, select **Admin**.</span><span class="sxs-lookup"><span data-stu-id="8320a-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="8320a-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="8320a-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="8320a-166">Perform the following steps on **AUTHENTICATION** section.</span><span class="sxs-lookup"><span data-stu-id="8320a-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="8320a-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8320a-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="8320a-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="8320a-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="8320a-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="8320a-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="8320a-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="8320a-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="8320a-172">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8320a-172">Click **Save** button.</span></span>
9. <span data-ttu-id="8320a-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8320a-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="8320a-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8320a-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8320a-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8320a-177">Create an Azure AD test user</span></span>
<span data-ttu-id="8320a-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8320a-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="8320a-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8320a-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8320a-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8320a-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="8320a-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8320a-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8320a-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8320a-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="8320a-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8320a-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="8320a-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8320a-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="8320a-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8320a-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="8320a-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8320a-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="8320a-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8320a-192">Click **Next**.</span></span>
6. <span data-ttu-id="8320a-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8320a-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="8320a-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8320a-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="8320a-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8320a-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="8320a-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8320a-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="8320a-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8320a-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="8320a-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8320a-199">Click **Next**.</span></span>
7. <span data-ttu-id="8320a-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8320a-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="8320a-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8320a-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="8320a-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8320a-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="8320a-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8320a-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="8320a-206">Create a Wizergos Productivity Software test user</span><span class="sxs-lookup"><span data-stu-id="8320a-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="8320a-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="8320a-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="8320a-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span><span class="sxs-lookup"><span data-stu-id="8320a-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8320a-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8320a-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="8320a-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="8320a-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Assign User][200]

<span data-ttu-id="8320a-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8320a-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8320a-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8320a-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="8320a-215">In the applications list, select **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="8320a-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="8320a-217">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8320a-217">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="8320a-219">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8320a-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8320a-220">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8320a-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8320a-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8320a-222">Test single sign-on</span></span>
<span data-ttu-id="8320a-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8320a-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8320a-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span><span class="sxs-lookup"><span data-stu-id="8320a-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8320a-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8320a-225">Additional resources</span></span>
* [<span data-ttu-id="8320a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8320a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8320a-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8320a-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png




























