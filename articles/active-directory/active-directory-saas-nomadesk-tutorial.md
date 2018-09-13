---
title: 'Tutorial: Azure Active Directory integration with Nomadesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nomadesk.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 55a80ed1655695c4a80aa1a8e57ad71880d8dbf6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661530"
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="50079-103">Tutorial: Azure Active Directory integration with Nomadesk</span><span class="sxs-lookup"><span data-stu-id="50079-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>
<span data-ttu-id="50079-104">The objective of this tutorial is to show you how to integrate Nomadesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50079-104">The objective of this tutorial is to show you how to integrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50079-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="50079-105">Integrating Nomadesk with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="50079-106">You can control in Azure AD who has access to Nomadesk</span><span class="sxs-lookup"><span data-stu-id="50079-106">You can control in Azure AD who has access to Nomadesk</span></span>
* <span data-ttu-id="50079-107">You can enable your users to automatically get signed-on to Nomadesk single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="50079-107">You can enable your users to automatically get signed-on to Nomadesk single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="50079-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="50079-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="50079-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50079-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50079-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50079-110">Prerequisites</span></span>
<span data-ttu-id="50079-111">To configure Azure AD integration with Nomadesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="50079-111">To configure Azure AD integration with Nomadesk, you need the following items:</span></span>

* <span data-ttu-id="50079-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="50079-112">An Azure AD subscription</span></span>
* <span data-ttu-id="50079-113">A Nomadesk single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="50079-113">A Nomadesk single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="50079-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="50079-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="50079-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="50079-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="50079-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="50079-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="50079-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50079-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50079-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="50079-118">Scenario Description</span></span>
<span data-ttu-id="50079-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="50079-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="50079-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="50079-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50079-121">Adding Nomadesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="50079-121">Adding Nomadesk from the gallery</span></span>
2. <span data-ttu-id="50079-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="50079-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-nomadesk-from-the-gallery"></a><span data-ttu-id="50079-123">Add Nomadesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="50079-123">Add Nomadesk from the gallery</span></span>
<span data-ttu-id="50079-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="50079-124">To configure the integration of Nomadesk into Azure AD, you need to add Nomadesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50079-125">**To add Nomadesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50079-125">**To add Nomadesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50079-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50079-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="50079-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="50079-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="50079-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="50079-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="50079-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="50079-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="50079-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="50079-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="50079-135">In the search box, type **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="50079-135">In the search box, type **Nomadesk**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_01.png)
7. <span data-ttu-id="50079-137">In the results pane, select **Nomadesk**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="50079-137">In the results pane, select **Nomadesk**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="50079-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="50079-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="50079-140">The objective of this section is to show you how to configure and test Azure AD SSO with Nomadesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="50079-140">The objective of this section is to show you how to configure and test Azure AD SSO with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50079-141">For SSO to work, Azure AD needs to know what the counterpart user in Nomadesk to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="50079-141">For SSO to work, Azure AD needs to know what the counterpart user in Nomadesk to an user in Azure AD is.</span></span> <span data-ttu-id="50079-142">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="50079-142">In other words, a link relationship between an Azure AD user and the related user in Nomadesk needs to be established.</span></span>

<span data-ttu-id="50079-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="50079-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Nomadesk.</span></span>

<span data-ttu-id="50079-144">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="50079-144">To configure and test Azure AD single sign-on with Nomadesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50079-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="50079-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50079-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50079-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50079-147">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="50079-147">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - to have a counterpart of Britta Simon in Nomadesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="50079-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="50079-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50079-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="50079-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="50079-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="50079-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="50079-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Nomadesk application.</span><span class="sxs-lookup"><span data-stu-id="50079-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Nomadesk application.</span></span>

<span data-ttu-id="50079-152">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50079-152">**To configure Azure AD single sign-on with Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="50079-153">In the Azure classic portal, on the **Nomadesk** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="50079-153">In the Azure classic portal, on the **Nomadesk** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="50079-155">On the **How would you like users to sign on to Nomadesk** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50079-155">On the **How would you like users to sign on to Nomadesk** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_03.png)
3. <span data-ttu-id="50079-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50079-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_04.png)
  * <span data-ttu-id="50079-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Nomadesk application using the following pattern: **“https://mynomadesk.com/logon/saml/TENANTID”**.</span><span class="sxs-lookup"><span data-stu-id="50079-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Nomadesk application using the following pattern: **“https://mynomadesk.com/logon/saml/TENANTID”**.</span></span> <span data-ttu-id="50079-160">When referencing a generic name that **TENANTID** needs to be replaced by an actual tenant id .</span><span class="sxs-lookup"><span data-stu-id="50079-160">When referencing a generic name that **TENANTID** needs to be replaced by an actual tenant id .</span></span>
4. <span data-ttu-id="50079-161">On the **Configure single sign-on at Nomadesk** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50079-161">On the **Configure single sign-on at Nomadesk** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_05.png)
  1. <span data-ttu-id="50079-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="50079-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="50079-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50079-164">Click **Next**.</span></span>
5. <span data-ttu-id="50079-165">To get SSO configured for your application, contact your Nomadesk support team via support@nomadesk.com.</span><span class="sxs-lookup"><span data-stu-id="50079-165">To get SSO configured for your application, contact your Nomadesk support team via support@nomadesk.com.</span></span> <span data-ttu-id="50079-166">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Nomadesk team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="50079-166">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Nomadesk team to set up SSO on their side.</span></span>
6. <span data-ttu-id="50079-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50079-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="50079-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="50079-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50079-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="50079-171">Create an Azure AD test user</span></span>
<span data-ttu-id="50079-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50079-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="50079-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50079-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50079-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50079-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="50079-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="50079-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="50079-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="50079-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="50079-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="50079-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="50079-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50079-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="50079-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="50079-184">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="50079-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50079-185">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="50079-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50079-186">Click **Next**.</span></span>
6. <span data-ttu-id="50079-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50079-187">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_06.png)
 1. <span data-ttu-id="50079-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="50079-189">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="50079-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="50079-190">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="50079-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="50079-191">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="50079-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="50079-192">In the **Role** list, select **User**.</span></span>  
 5. <span data-ttu-id="50079-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="50079-193">Click **Next**.</span></span>
7. <span data-ttu-id="50079-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="50079-194">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="50079-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="50079-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="50079-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="50079-198">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="50079-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="50079-199">Click **Complete**.</span></span>   

### <a name="create-a-nomadesk-test-user"></a><span data-ttu-id="50079-200">Create a Nomadesk test user</span><span class="sxs-lookup"><span data-stu-id="50079-200">Create a Nomadesk test user</span></span>
<span data-ttu-id="50079-201">The objective of this section is to create a user called Britta Simon in Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="50079-201">The objective of this section is to create a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="50079-202">Nomadesk supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="50079-202">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="50079-203">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="50079-203">There is no action item for you in this section.</span></span> <span data-ttu-id="50079-204">A new user will be created during an attempt to access Nomadesk if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="50079-204">A new user will be created during an attempt to access Nomadesk if it doesn't exist yet.</span></span> <span data-ttu-id="50079-205">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="50079-205">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="50079-206">If you need to create an user manually, you need to contact the Nomadesk support team.</span><span class="sxs-lookup"><span data-stu-id="50079-206">If you need to create an user manually, you need to contact the Nomadesk support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="50079-207">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="50079-207">Assign the Azure AD test user</span></span>
<span data-ttu-id="50079-208">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="50079-208">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Nomadesk.</span></span>

![Assign User][200]

<span data-ttu-id="50079-210">**To assign Britta Simon to Nomadesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="50079-210">**To assign Britta Simon to Nomadesk, perform the following steps:**</span></span>

1. <span data-ttu-id="50079-211">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="50079-211">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="50079-213">In the applications list, select **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="50079-213">In the applications list, select **Nomadesk**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_50.png)
3. <span data-ttu-id="50079-215">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="50079-215">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="50079-217">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="50079-217">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="50079-218">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="50079-218">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="50079-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="50079-220">Test single sign-on</span></span>
<span data-ttu-id="50079-221">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="50079-221">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="50079-222">When you click the Nomadesk tile in the Access Panel, you should get automatically signed-on to your Nomadesk application.</span><span class="sxs-lookup"><span data-stu-id="50079-222">When you click the Nomadesk tile in the Access Panel, you should get automatically signed-on to your Nomadesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50079-223">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="50079-223">Additional Resources</span></span>
* [<span data-ttu-id="50079-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50079-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50079-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50079-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-nomadesk-tutorial/tutorial_general_205.png

























