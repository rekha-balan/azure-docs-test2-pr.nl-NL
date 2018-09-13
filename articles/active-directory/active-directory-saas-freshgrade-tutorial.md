---
title: 'Tutorial: Azure Active Directory integration with FreshGrade | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FreshGrade.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: f6367e3ef5a95cdfd78794ed5e7071a03759f47f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548957"
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="e9794-103">Tutorial: Azure Active Directory integration with FreshGrade</span><span class="sxs-lookup"><span data-stu-id="e9794-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>
<span data-ttu-id="e9794-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9794-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9794-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e9794-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e9794-106">You can control in Azure AD who has access to FreshGrade- You can enable your users to automatically get signed-on to FreshGrade single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e9794-106">You can control in Azure AD who has access to FreshGrade- You can enable your users to automatically get signed-on to FreshGrade single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="e9794-107">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e9794-107">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e9794-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9794-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9794-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9794-109">Prerequisites</span></span>
<span data-ttu-id="e9794-110">To configure Azure AD integration with FreshGrade, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e9794-110">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

* <span data-ttu-id="e9794-111">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e9794-111">An Azure AD subscription</span></span>
* <span data-ttu-id="e9794-112">A FreshGrade SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e9794-112">A FreshGrade SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="e9794-113">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e9794-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="e9794-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e9794-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e9794-115">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e9794-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e9794-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9794-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9794-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e9794-117">Scenario description</span></span>
<span data-ttu-id="e9794-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e9794-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e9794-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9794-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9794-120">Adding FreshGrade from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9794-120">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="e9794-121">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9794-121">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-freshgrade-from-the-gallery"></a><span data-ttu-id="e9794-122">Add FreshGrade from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9794-122">Add FreshGrade from the gallery</span></span>
<span data-ttu-id="e9794-123">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e9794-123">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9794-124">**To add FreshGrade from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9794-124">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9794-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9794-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="e9794-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9794-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9794-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9794-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="e9794-130">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e9794-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e9794-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e9794-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="e9794-134">In the search box, type **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="e9794-134">In the search box, type **FreshGrade**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_01.png)
7. <span data-ttu-id="e9794-136">In the results pane, select **FreshGrade**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e9794-136">In the results pane, select **FreshGrade**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="e9794-137">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9794-137">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="e9794-138">In this section, you configure and test Azure AD SSO with FreshGrade based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9794-138">In this section, you configure and test Azure AD SSO with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9794-139">For SSO to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9794-139">For SSO to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="e9794-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e9794-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="e9794-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e9794-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshGrade.</span></span>

<span data-ttu-id="e9794-142">To configure and test Azure AD SSO with FreshGrade, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9794-142">To configure and test Azure AD SSO with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9794-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e9794-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9794-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9794-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9794-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e9794-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e9794-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9794-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9794-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e9794-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="e9794-148">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9794-148">Configure Azure AD SSO</span></span>
<span data-ttu-id="e9794-149">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your FreshGrade application.</span><span class="sxs-lookup"><span data-stu-id="e9794-149">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your FreshGrade application.</span></span>

<span data-ttu-id="e9794-150">**To configure Azure AD SSO with FreshGrade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9794-150">**To configure Azure AD SSO with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="e9794-151">In the classic portal, on the **FreshGrade** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e9794-151">In the classic portal, on the **FreshGrade** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="e9794-153">On the **How would you like users to sign on to FreshGrade** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9794-153">On the **How would you like users to sign on to FreshGrade** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_03.png) 
3. <span data-ttu-id="e9794-155">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9794-155">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_04.png) 
  1. <span data-ttu-id="e9794-157">In the **SIGN ON URL** textbox, type a URL using the following pattern:`https://<your-subdomain>.freshgrade.com` or `https://<your-subdomain>.onboarding.freshgrade.com`.</span><span class="sxs-lookup"><span data-stu-id="e9794-157">In the **SIGN ON URL** textbox, type a URL using the following pattern:`https://<your-subdomain>.freshgrade.com` or `https://<your-subdomain>.onboarding.freshgrade.com`.</span></span>
  2. <span data-ttu-id="e9794-158">click **Next**</span><span class="sxs-lookup"><span data-stu-id="e9794-158">click **Next**</span></span>
4. <span data-ttu-id="e9794-159">On the **Configure single sign-on at FreshGrade** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9794-159">On the **Configure single sign-on at FreshGrade** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_05.png)
  3. <span data-ttu-id="e9794-161">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e9794-161">Click **Download metadata**, and then save the file on your computer.</span></span>
5. <span data-ttu-id="e9794-162">To get SSO configured for your application, contact your support team at [Support@freshgrade.com](mailTo:support@freshgrade.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="e9794-162">To get SSO configured for your application, contact your support team at [Support@freshgrade.com](mailTo:support@freshgrade.com) and provide them with the following:</span></span>
   
  * <span data-ttu-id="e9794-163">The **Downloaded metadata**</span><span class="sxs-lookup"><span data-stu-id="e9794-163">The **Downloaded metadata**</span></span>
  * <span data-ttu-id="e9794-164">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="e9794-164">The **SAML SSO URL**</span></span>
6. <span data-ttu-id="e9794-165">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9794-165">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="e9794-167">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9794-167">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-a-azure-ad-test-user"></a><span data-ttu-id="e9794-169">Create a Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9794-169">Create a Azure AD test user</span></span>
<span data-ttu-id="e9794-170">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9794-170">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="e9794-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9794-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9794-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9794-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="e9794-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9794-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9794-176">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9794-176">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="e9794-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e9794-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="e9794-180">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9794-180">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="e9794-182">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e9794-182">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="e9794-183">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9794-183">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="e9794-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9794-184">Click **Next**.</span></span>
6. <span data-ttu-id="e9794-185">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9794-185">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="e9794-187">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e9794-187">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="e9794-188">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9794-188">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="e9794-189">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9794-189">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="e9794-190">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e9794-190">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="e9794-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9794-191">Click **Next**.</span></span>
7. <span data-ttu-id="e9794-192">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e9794-192">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="e9794-194">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9794-194">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="e9794-196">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e9794-196">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="e9794-197">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9794-197">Click **Complete**.</span></span>   

### <a name="create-a-freshgrade-test-user"></a><span data-ttu-id="e9794-198">Create a FreshGrade test user</span><span class="sxs-lookup"><span data-stu-id="e9794-198">Create a FreshGrade test user</span></span>
<span data-ttu-id="e9794-199">In this section, you create a user called Britta Simon in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e9794-199">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="e9794-200">Please work with FreshGrade support team to add the users in the FreshGrade platform.</span><span class="sxs-lookup"><span data-stu-id="e9794-200">Please work with FreshGrade support team to add the users in the FreshGrade platform.</span></span>
<span data-ttu-id="e9794-201">For any issues with creating users please contact [support@freshgrade.com](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="e9794-201">For any issues with creating users please contact [support@freshgrade.com](mailTo:support@freshgrade.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9794-202">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9794-202">Assign the Azure AD test user</span></span>
<span data-ttu-id="e9794-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="e9794-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FreshGrade.</span></span>

![Assign User][200] 

<span data-ttu-id="e9794-205">**To assign Britta Simon to FreshGrade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9794-205">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="e9794-206">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9794-206">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="e9794-208">In the applications list, select **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="e9794-208">In the applications list, select **FreshGrade**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_50.png) 
3. <span data-ttu-id="e9794-210">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9794-210">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="e9794-212">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9794-212">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e9794-213">In the tool.</span><span class="sxs-lookup"><span data-stu-id="e9794-213">In the tool.</span></span>
6. <span data-ttu-id="e9794-214">bar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e9794-214">bar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="e9794-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9794-216">Test single sign-on</span></span>
<span data-ttu-id="e9794-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e9794-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9794-218">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span><span class="sxs-lookup"><span data-stu-id="e9794-218">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9794-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9794-219">Additional resources</span></span>
* [<span data-ttu-id="e9794-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9794-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9794-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9794-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshgrade-tutorial/tutorial_general_205.png
























