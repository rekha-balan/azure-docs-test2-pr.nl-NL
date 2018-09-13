---
title: 'Tutorial: Azure Active Directory integration with Workrite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workrite.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2017
ms.author: jeedes
ms.openlocfilehash: cb4de6671565c903fd0bb789bff0baf7a4b5c422
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554422"
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="8df26-103">Tutorial: Azure Active Directory integration with Workrite</span><span class="sxs-lookup"><span data-stu-id="8df26-103">Tutorial: Azure Active Directory integration with Workrite</span></span>
<span data-ttu-id="8df26-104">The objective of this tutorial is to show you how to integrate Workrite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8df26-104">The objective of this tutorial is to show you how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8df26-105">Integrating Workrite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8df26-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="8df26-106">You can control in Azure AD who has access to Workrite</span><span class="sxs-lookup"><span data-stu-id="8df26-106">You can control in Azure AD who has access to Workrite</span></span> 
* <span data-ttu-id="8df26-107">You can enable your users to automatically get signed-on to Workrite single sign-on) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8df26-107">You can enable your users to automatically get signed-on to Workrite single sign-on) with their Azure AD accounts</span></span>
* <span data-ttu-id="8df26-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8df26-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8df26-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8df26-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8df26-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8df26-110">Prerequisites</span></span>
<span data-ttu-id="8df26-111">To configure Azure AD integration with Workrite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8df26-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

* <span data-ttu-id="8df26-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8df26-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8df26-113">A Workrite single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8df26-113">A Workrite single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="8df26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8df26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="8df26-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8df26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8df26-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8df26-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8df26-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8df26-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8df26-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="8df26-118">Scenario Description</span></span>
<span data-ttu-id="8df26-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8df26-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="8df26-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8df26-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="8df26-121">Adding Workrite from the gallery</span><span class="sxs-lookup"><span data-stu-id="8df26-121">Adding Workrite from the gallery</span></span> 
2. <span data-ttu-id="8df26-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8df26-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="8df26-123">Adding Workrite from the gallery</span><span class="sxs-lookup"><span data-stu-id="8df26-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="8df26-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8df26-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8df26-125">**To add Workrite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df26-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8df26-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8df26-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="8df26-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8df26-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8df26-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8df26-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="8df26-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8df26-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="8df26-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8df26-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="8df26-135">In the search box, type **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="8df26-135">In the search box, type **Workrite**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="8df26-137">In the results pane, select **Workrite**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8df26-137">In the results pane, select **Workrite**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][500]

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="8df26-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8df26-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="8df26-140">The objective of this section is to show you how to configure and test Azure AD SSO with Workrite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8df26-140">The objective of this section is to show you how to configure and test Azure AD SSO with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8df26-141">For SSO to work, Azure AD needs to know what the counterpart user in Workrite to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="8df26-141">For SSO to work, Azure AD needs to know what the counterpart user in Workrite to an user in Azure AD is.</span></span> <span data-ttu-id="8df26-142">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8df26-142">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>  

<span data-ttu-id="8df26-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workrite.</span><span class="sxs-lookup"><span data-stu-id="8df26-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workrite.</span></span>

<span data-ttu-id="8df26-144">To configure and test Azure AD SSO with Workrite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8df26-144">To configure and test Azure AD SSO with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8df26-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8df26-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8df26-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8df26-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8df26-147">**[Creating a Workrite test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8df26-147">**[Creating a Workrite test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8df26-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8df26-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8df26-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8df26-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="8df26-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8df26-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="8df26-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Workrite application.</span><span class="sxs-lookup"><span data-stu-id="8df26-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Workrite application.</span></span>

<span data-ttu-id="8df26-152">**To configure Azure AD SSO with Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df26-152">**To configure Azure AD SSO with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="8df26-153">In the Azure classic portal, on the **Workrite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="8df26-153">In the Azure classic portal, on the **Workrite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="8df26-155">On the **How would you like users to sign on to Workrite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-155">On the **How would you like users to sign on to Workrite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="8df26-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8] 
  1. <span data-ttu-id="8df26-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Workrite site (e.g.: *https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=1a82b5aa-4dd6-4472-9721-7d0193f59e22*).</span><span class="sxs-lookup"><span data-stu-id="8df26-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Workrite site (e.g.: *https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=1a82b5aa-4dd6-4472-9721-7d0193f59e22*).</span></span>

    >[!NOTE]
    ><span data-ttu-id="8df26-160">Please contact your Workrite support team [support@workrite.co.uk](mailto:support@workrite.co.uk) if you don't know the value of the Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="8df26-160">Please contact your Workrite support team [support@workrite.co.uk](mailto:support@workrite.co.uk) if you don't know the value of the Sign On URL.</span></span> 
    >   
  2. <span data-ttu-id="8df26-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-161">Click **Next**.</span></span>
4. <span data-ttu-id="8df26-162">On the **Configure single sign-on at Workrite** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-162">On the **Configure single sign-on at Workrite** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9] 
 1. <span data-ttu-id="8df26-164">Click Download certificate, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8df26-164">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="8df26-165">Contact your Workrite support team [support@workrite.co.uk](mailto:support@workrite.co.uk), peovide them with the downloaded certificate, the **Issuer URL** (Entity ID), the **Single Sign-On Service URL**, the **Single Sign-Out URL**, and then ask them to setup SSO for your Workrite app.</span><span class="sxs-lookup"><span data-stu-id="8df26-165">Contact your Workrite support team [support@workrite.co.uk](mailto:support@workrite.co.uk), peovide them with the downloaded certificate, the **Issuer URL** (Entity ID), the **Single Sign-On Service URL**, the **Single Sign-Out URL**, and then ask them to setup SSO for your Workrite app.</span></span>  
 3. <span data-ttu-id="8df26-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-166">Click **Next**.</span></span>
5. <span data-ttu-id="8df26-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
6. <span data-ttu-id="8df26-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8df26-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8df26-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8df26-171">Create an Azure AD test user</span></span>
<span data-ttu-id="8df26-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8df26-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="8df26-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df26-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8df26-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8df26-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="8df26-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8df26-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8df26-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8df26-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="8df26-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8df26-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="8df26-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="8df26-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8df26-184">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="8df26-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8df26-185">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="8df26-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-186">Click **Next**.</span></span>
6. <span data-ttu-id="8df26-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-187">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="8df26-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8df26-189">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="8df26-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8df26-190">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="8df26-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8df26-191">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="8df26-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8df26-192">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="8df26-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8df26-193">Click **Next**.</span></span>
7. <span data-ttu-id="8df26-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8df26-194">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="8df26-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="8df26-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8df26-198">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="8df26-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8df26-199">Click **Complete**.</span></span>   

### <a name="create-a-workrite-test-user"></a><span data-ttu-id="8df26-200">Create a Workrite test user</span><span class="sxs-lookup"><span data-stu-id="8df26-200">Create a Workrite test user</span></span>
<span data-ttu-id="8df26-201">The objective of this section is to create a user called Britta Simon in Workrite.</span><span class="sxs-lookup"><span data-stu-id="8df26-201">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="8df26-202">**To create a user called Britta Simon in Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df26-202">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="8df26-203">Sign on to your workrite company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="8df26-203">Sign on to your workrite company site as administrator.</span></span>
2. <span data-ttu-id="8df26-204">In the navigation pane, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="8df26-204">In the navigation pane, click **Admin**.</span></span>
   
    ![Assign User][400]
3. <span data-ttu-id="8df26-206">Go to Quick Links, and then click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="8df26-206">Go to Quick Links, and then click **Create User**.</span></span> 
   
    ![Assign User][401]
4. <span data-ttu-id="8df26-208">On the **Create User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df26-208">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Assign User][402]
 1. <span data-ttu-id="8df26-210">Type the **Email**, the **First Name** and the **Surname** of a valid Azure AD user you want to provision.</span><span class="sxs-lookup"><span data-stu-id="8df26-210">Type the **Email**, the **First Name** and the **Surname** of a valid Azure AD user you want to provision.</span></span>  
 2. <span data-ttu-id="8df26-211">Select **Client Administrator** as **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="8df26-211">Select **Client Administrator** as **Choose Role**.</span></span>  
 3. <span data-ttu-id="8df26-212">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8df26-212">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8df26-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8df26-213">Assign the Azure AD test user</span></span>
<span data-ttu-id="8df26-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Workrite.</span><span class="sxs-lookup"><span data-stu-id="8df26-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Workrite.</span></span>

    ![Assign User][200] 

<span data-ttu-id="8df26-215">**To assign Britta Simon to Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df26-215">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="8df26-216">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8df26-216">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="8df26-218">In the applications list, select **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="8df26-218">In the applications list, select **Workrite**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="8df26-220">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8df26-220">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="8df26-222">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8df26-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8df26-223">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8df26-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8df26-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8df26-225">Test single sign-on</span></span>
<span data-ttu-id="8df26-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8df26-226">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8df26-227">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span><span class="sxs-lookup"><span data-stu-id="8df26-227">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8df26-228">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="8df26-228">Additional Resources</span></span>
* [<span data-ttu-id="8df26-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8df26-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8df26-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8df26-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_01.png
[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_05.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_02.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_07.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_general_205.png


[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png
































