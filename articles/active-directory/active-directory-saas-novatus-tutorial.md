---
title: 'Tutorial: Azure Active Directory integration with Novatus | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Novatus.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 26abf35a9c5335e1bff7e2899f40323a0e12d590
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554415"
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="26f97-103">Tutorial: Azure Active Directory integration with Novatus</span><span class="sxs-lookup"><span data-stu-id="26f97-103">Tutorial: Azure Active Directory integration with Novatus</span></span>
<span data-ttu-id="26f97-104">The objective of this tutorial is to show you how to integrate Novatus with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26f97-104">The objective of this tutorial is to show you how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26f97-105">Integrating Novatus with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="26f97-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="26f97-106">You can control in Azure AD who has access to Novatus</span><span class="sxs-lookup"><span data-stu-id="26f97-106">You can control in Azure AD who has access to Novatus</span></span>
* <span data-ttu-id="26f97-107">You can enable your users to automatically get signed-on to Novatus single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="26f97-107">You can enable your users to automatically get signed-on to Novatus single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="26f97-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="26f97-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="26f97-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26f97-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26f97-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26f97-110">Prerequisites</span></span>
<span data-ttu-id="26f97-111">To configure Azure AD integration with Novatus, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="26f97-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

* <span data-ttu-id="26f97-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="26f97-112">An Azure AD subscription</span></span>
* <span data-ttu-id="26f97-113">A Novatus single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="26f97-113">A Novatus single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="26f97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="26f97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="26f97-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="26f97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="26f97-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="26f97-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="26f97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26f97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26f97-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="26f97-118">Scenario Description</span></span>
<span data-ttu-id="26f97-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="26f97-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="26f97-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="26f97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="26f97-121">Adding Novatus from the gallery</span><span class="sxs-lookup"><span data-stu-id="26f97-121">Adding Novatus from the gallery</span></span>
* <span data-ttu-id="26f97-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26f97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-novatus-from-the-gallery"></a><span data-ttu-id="26f97-123">Add Novatus from the gallery</span><span class="sxs-lookup"><span data-stu-id="26f97-123">Add Novatus from the gallery</span></span>
<span data-ttu-id="26f97-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="26f97-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26f97-125">**To add Novatus from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26f97-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26f97-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26f97-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="26f97-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="26f97-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="26f97-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="26f97-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="26f97-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="26f97-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="26f97-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="26f97-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="26f97-135">In the search box, type **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="26f97-135">In the search box, type **Novatus**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_01.png)
7. <span data-ttu-id="26f97-137">In the results pane, select **Novatus**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="26f97-137">In the results pane, select **Novatus**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26f97-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26f97-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="26f97-140">The objective of this section is to show you how to configure and test Azure AD SSO with Novatus based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26f97-140">The objective of this section is to show you how to configure and test Azure AD SSO with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26f97-141">For SSO to work, Azure AD needs to know what the counterpart user in Novatus to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="26f97-141">For SSO to work, Azure AD needs to know what the counterpart user in Novatus to an user in Azure AD is.</span></span> <span data-ttu-id="26f97-142">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span><span class="sxs-lookup"><span data-stu-id="26f97-142">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="26f97-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Novatus.</span><span class="sxs-lookup"><span data-stu-id="26f97-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Novatus.</span></span>

<span data-ttu-id="26f97-144">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="26f97-144">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26f97-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="26f97-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26f97-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26f97-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26f97-147">**[Creating a Novatus test user](#creating-a-Novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="26f97-147">**[Creating a Novatus test user](#creating-a-Novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="26f97-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="26f97-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26f97-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="26f97-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26f97-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26f97-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="26f97-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Novatus application.</span><span class="sxs-lookup"><span data-stu-id="26f97-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Novatus application.</span></span>

<span data-ttu-id="26f97-152">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26f97-152">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="26f97-153">In the Azure classic portal, on the **Novatus** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="26f97-153">In the Azure classic portal, on the **Novatus** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="26f97-155">On the **How would you like users to sign on to Novatus** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26f97-155">On the **How would you like users to sign on to Novatus** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_03.png) 
3. <span data-ttu-id="26f97-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26f97-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_04.png) 
  * <span data-ttu-id="26f97-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Novatus application using the following pattern: **“https://sso.novatuscontracts.com/companyname”**.</span><span class="sxs-lookup"><span data-stu-id="26f97-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Novatus application using the following pattern: **“https://sso.novatuscontracts.com/companyname”**.</span></span> <span data-ttu-id="26f97-160">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span><span class="sxs-lookup"><span data-stu-id="26f97-160">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
4. <span data-ttu-id="26f97-161">On the **Configure single sign-on at Novatus** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26f97-161">On the **Configure single sign-on at Novatus** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_05.png)   
  1. <span data-ttu-id="26f97-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="26f97-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="26f97-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26f97-164">Click **Next**.</span></span>
5. <span data-ttu-id="26f97-165">To get SSO configured for your application, contact your Novatus support team via jvinci@novatusinc.com.</span><span class="sxs-lookup"><span data-stu-id="26f97-165">To get SSO configured for your application, contact your Novatus support team via jvinci@novatusinc.com.</span></span> <span data-ttu-id="26f97-166">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Novatus team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="26f97-166">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Novatus team to set up SSO on their side.</span></span>
6. <span data-ttu-id="26f97-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26f97-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="26f97-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="26f97-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26f97-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="26f97-171">Create an Azure AD test user</span></span>
<span data-ttu-id="26f97-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26f97-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="26f97-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26f97-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26f97-175">In the **Azure classic p ortal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26f97-175">In the **Azure classic p ortal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="26f97-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="26f97-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="26f97-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="26f97-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="26f97-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="26f97-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="26f97-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26f97-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="26f97-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="26f97-184">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="26f97-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26f97-185">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="26f97-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26f97-186">Click **Next**.</span></span>
6. <span data-ttu-id="26f97-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26f97-187">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="26f97-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="26f97-189">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="26f97-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="26f97-190">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="26f97-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="26f97-191">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="26f97-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="26f97-192">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="26f97-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="26f97-193">Click **Next**.</span></span>
7. <span data-ttu-id="26f97-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="26f97-194">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="26f97-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26f97-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="26f97-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="26f97-198">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="26f97-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="26f97-199">Click **Complete**.</span></span>   

### <a name="create-a-novatus-test-user"></a><span data-ttu-id="26f97-200">Create a Novatus test user</span><span class="sxs-lookup"><span data-stu-id="26f97-200">Create a Novatus test user</span></span>
<span data-ttu-id="26f97-201">The objective of this section is to create a user called Britta Simon in Novatus.</span><span class="sxs-lookup"><span data-stu-id="26f97-201">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="26f97-202">Novatus supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="26f97-202">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="26f97-203">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="26f97-203">There is no action item for you in this section.</span></span> <span data-ttu-id="26f97-204">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="26f97-204">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span> <span data-ttu-id="26f97-205">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="26f97-205">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="26f97-206">If you need to create an user manually, you need to contact the Novatus support team.</span><span class="sxs-lookup"><span data-stu-id="26f97-206">If you need to create an user manually, you need to contact the Novatus support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="26f97-207">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="26f97-207">Assign the Azure AD test user</span></span>
<span data-ttu-id="26f97-208">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Novatus.</span><span class="sxs-lookup"><span data-stu-id="26f97-208">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Novatus.</span></span>

![Assign User][200] 

<span data-ttu-id="26f97-210">**To assign Britta Simon to Novatus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26f97-210">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="26f97-211">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="26f97-211">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="26f97-213">In the applications list, select **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="26f97-213">In the applications list, select **Novatus**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_novatus_50.png) 
3. <span data-ttu-id="26f97-215">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="26f97-215">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="26f97-217">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="26f97-217">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="26f97-218">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="26f97-218">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="26f97-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="26f97-220">Test single sign-on</span></span>
<span data-ttu-id="26f97-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="26f97-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="26f97-222">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span><span class="sxs-lookup"><span data-stu-id="26f97-222">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26f97-223">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="26f97-223">Additional Resources</span></span>
* [<span data-ttu-id="26f97-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26f97-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26f97-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26f97-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-novatus-tutorial/tutorial_general_205.png

























