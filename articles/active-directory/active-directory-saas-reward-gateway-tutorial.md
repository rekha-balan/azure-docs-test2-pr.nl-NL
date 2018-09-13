---
title: 'Tutorial: Azure Active Directory integration with Reward Gateway | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Reward Gateway.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: f7f38b07190babd9920e7ac5670770f9b6c0a97a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563722"
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="de54e-103">Tutorial: Azure Active Directory integration with Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="de54e-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>
<span data-ttu-id="de54e-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de54e-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de54e-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="de54e-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="de54e-106">You can control in Azure AD who has access to Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="de54e-106">You can control in Azure AD who has access to Reward Gateway</span></span>
* <span data-ttu-id="de54e-107">You can enable your users to automatically get signed-on to Reward Gateway single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="de54e-107">You can enable your users to automatically get signed-on to Reward Gateway single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="de54e-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="de54e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="de54e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de54e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de54e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="de54e-110">Prerequisites</span></span>
<span data-ttu-id="de54e-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="de54e-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

* <span data-ttu-id="de54e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="de54e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="de54e-113">A Reward Gateway SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="de54e-113">A Reward Gateway SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="de54e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="de54e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="de54e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="de54e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="de54e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="de54e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="de54e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de54e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de54e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="de54e-118">Scenario description</span></span>
<span data-ttu-id="de54e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="de54e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="de54e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="de54e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de54e-121">Adding Reward Gateway from the gallery</span><span class="sxs-lookup"><span data-stu-id="de54e-121">Adding Reward Gateway from the gallery</span></span>
2. <span data-ttu-id="de54e-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="de54e-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-reward-gateway-from-the-gallery"></a><span data-ttu-id="de54e-123">Add Reward Gateway from the gallery</span><span class="sxs-lookup"><span data-stu-id="de54e-123">Add Reward Gateway from the gallery</span></span>
<span data-ttu-id="de54e-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="de54e-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de54e-125">**To add Reward Gateway from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de54e-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de54e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de54e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="de54e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="de54e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="de54e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="de54e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="de54e-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="de54e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="de54e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="de54e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="de54e-135">In the search box, type **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="de54e-135">In the search box, type **Reward Gateway**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_01.png)
7. <span data-ttu-id="de54e-137">In the results pane, select **Reward Gateway**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="de54e-137">In the results pane, select **Reward Gateway**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="de54e-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="de54e-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="de54e-140">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de54e-140">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de54e-141">For SSO to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de54e-141">For SSO to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="de54e-142">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span><span class="sxs-lookup"><span data-stu-id="de54e-142">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="de54e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="de54e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Reward Gateway.</span></span>

<span data-ttu-id="de54e-144">To configure and test Azure AD SSO with Reward Gateway, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="de54e-144">To configure and test Azure AD SSO with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de54e-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="de54e-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de54e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de54e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de54e-147">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="de54e-147">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="de54e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="de54e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de54e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="de54e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="de54e-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="de54e-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="de54e-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Reward Gateway application.</span><span class="sxs-lookup"><span data-stu-id="de54e-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Reward Gateway application.</span></span>

<span data-ttu-id="de54e-152">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de54e-152">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="de54e-153">In the classic portal, on the **Reward Gateway** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="de54e-153">In the classic portal, on the **Reward Gateway** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="de54e-155">On the **How would you like users to sign on to Reward Gateway** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="de54e-155">On the **How would you like users to sign on to Reward Gateway** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_03.png) 
3. <span data-ttu-id="de54e-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de54e-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_04.png) 
  1. <span data-ttu-id="de54e-159">In the **Identifier URL** textbox, type the URL used by your users to sign-on to your Reward Gateway application using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="de54e-159">In the **Identifier URL** textbox, type the URL used by your users to sign-on to your Reward Gateway application using the following pattern:</span></span> 
   
    | <span data-ttu-id="de54e-160">Identifier URL</span><span class="sxs-lookup"><span data-stu-id="de54e-160">Identifier URL</span></span> |
    | --- |
    | `https://<company name>.rewardgateway.com/` |
    | `https://<company name>.rewardgateway.co.uk/` |
    | `https://<company name>.rewardgateway.co.nz/` |
    | `https://<company name>.rewardgateway.com.au/` |
  2. <span data-ttu-id="de54e-161">In the **Reply URL** textbox, type the URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="de54e-161">In the **Reply URL** textbox, type the URL using the following pattern:</span></span> 

    | <span data-ttu-id="de54e-162">Reply URL</span><span class="sxs-lookup"><span data-stu-id="de54e-162">Reply URL</span></span> |
    | --- |
    | `https://<company name>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<company name>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<company name>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<company name>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

  3. <span data-ttu-id="de54e-163">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="de54e-163">click **Next**.</span></span>

4. <span data-ttu-id="de54e-164">On the **Configure single sign-on at Reward Gateway** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de54e-164">On the **Configure single sign-on at Reward Gateway** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_05.png)
  * <span data-ttu-id="de54e-166">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="de54e-166">Click **Download metadata**, and then save the file on your computer.</span></span>
5. <span data-ttu-id="de54e-167">To get SSO configured for your application, contact Reward Gateway [support team](mailTo:clientsupport@rewardgateway.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="de54e-167">To get SSO configured for your application, contact Reward Gateway [support team](mailTo:clientsupport@rewardgateway.com) and provide them with the following:</span></span>
   
    <span data-ttu-id="de54e-168">• The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="de54e-168">• The downloaded **metadata**</span></span>
6. <span data-ttu-id="de54e-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="de54e-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
6. <span data-ttu-id="de54e-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="de54e-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="de54e-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="de54e-173">Create an Azure AD test user</span></span>
<span data-ttu-id="de54e-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de54e-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="de54e-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de54e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de54e-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de54e-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="de54e-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="de54e-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="de54e-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="de54e-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="de54e-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="de54e-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="de54e-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de54e-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_05.png)    
  1. <span data-ttu-id="de54e-186">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="de54e-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="de54e-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de54e-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="de54e-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="de54e-188">Click **Next**.</span></span>
6. <span data-ttu-id="de54e-189">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de54e-189">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_06.png)    
  1. <span data-ttu-id="de54e-191">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="de54e-191">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="de54e-192">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="de54e-192">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="de54e-193">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="de54e-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="de54e-194">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="de54e-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="de54e-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="de54e-195">Click **Next**.</span></span>
7. <span data-ttu-id="de54e-196">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="de54e-196">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="de54e-198">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de54e-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="de54e-200">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="de54e-200">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="de54e-201">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="de54e-201">Click **Complete**.</span></span>   

### <a name="create-an-reward-gateway-test-user"></a><span data-ttu-id="de54e-202">Create an Reward Gateway test user</span><span class="sxs-lookup"><span data-stu-id="de54e-202">Create an Reward Gateway test user</span></span>
<span data-ttu-id="de54e-203">In this section, you create a user called Britta Simon in Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="de54e-203">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="de54e-204">Please work with Reward Gateway [support team](mailTo:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span><span class="sxs-lookup"><span data-stu-id="de54e-204">Please work with Reward Gateway [support team](mailTo:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="de54e-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="de54e-205">Assign the Azure AD test user</span></span>
<span data-ttu-id="de54e-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="de54e-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Reward Gateway.</span></span>

![Assign User][200] 

<span data-ttu-id="de54e-208">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de54e-208">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="de54e-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="de54e-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="de54e-211">In the applications list, select **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="de54e-211">In the applications list, select **Reward Gateway**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_50.png) 
3. <span data-ttu-id="de54e-213">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="de54e-213">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="de54e-215">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="de54e-215">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="de54e-216">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="de54e-216">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="de54e-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="de54e-218">Test single sign-on</span></span>
<span data-ttu-id="de54e-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="de54e-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de54e-220">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span><span class="sxs-lookup"><span data-stu-id="de54e-220">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de54e-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="de54e-221">Additional resources</span></span>
* [<span data-ttu-id="de54e-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de54e-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de54e-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de54e-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-reward-gateway-tutorial/tutorial_general_205.png

























