---
title: 'Tutorial: Azure Active Directory integration with People | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and People.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 303152008189069a0f5d6228aab659173cee8da7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553698"
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="a1574-103">Tutorial: Azure Active Directory integration with People</span><span class="sxs-lookup"><span data-stu-id="a1574-103">Tutorial: Azure Active Directory integration with People</span></span>
<span data-ttu-id="a1574-104">The objective of this tutorial is to show you how to integrate People with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1574-104">The objective of this tutorial is to show you how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1574-105">Integrating People with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a1574-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="a1574-106">You can control in Azure AD who has access to People</span><span class="sxs-lookup"><span data-stu-id="a1574-106">You can control in Azure AD who has access to People</span></span>
* <span data-ttu-id="a1574-107">You can enable your users to automatically get signed-on to People single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a1574-107">You can enable your users to automatically get signed-on to People single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a1574-108">You can manage your accounts in one central location with the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="a1574-108">You can manage your accounts in one central location with the Azure classic portal</span></span>

<span data-ttu-id="a1574-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1574-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1574-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1574-110">Prerequisites</span></span>
<span data-ttu-id="a1574-111">To configure Azure AD integration with People, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a1574-111">To configure Azure AD integration with People, you need the following items:</span></span>

* <span data-ttu-id="a1574-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a1574-112">An Azure subscription</span></span>
* <span data-ttu-id="a1574-113">A People single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a1574-113">A People single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a1574-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a1574-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a1574-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a1574-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a1574-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="a1574-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a1574-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1574-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1574-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="a1574-118">Scenario Description</span></span>
<span data-ttu-id="a1574-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a1574-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="a1574-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1574-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1574-121">Adding People from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1574-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="a1574-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a1574-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-people-from-the-gallery"></a><span data-ttu-id="a1574-123">Add People from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1574-123">Add People from the gallery</span></span>
<span data-ttu-id="a1574-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a1574-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1574-125">**To add People from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1574-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1574-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1574-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a1574-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a1574-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a1574-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a1574-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="a1574-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a1574-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="a1574-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="a1574-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="a1574-135">In the search box, type **People**.</span><span class="sxs-lookup"><span data-stu-id="a1574-135">In the search box, type **People**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_01.png)
7. <span data-ttu-id="a1574-137">In the results pane, select **People**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="a1574-137">In the results pane, select **People**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a1574-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1574-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a1574-140">The objective of this section is to show you how to configure and test Azure AD SSO with People based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1574-140">The objective of this section is to show you how to configure and test Azure AD SSO with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1574-141">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1574-141">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1574-142">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a1574-142">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1574-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1574-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1574-144">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="a1574-144">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a1574-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1574-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1574-146">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a1574-146">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a1574-147">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1574-147">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="a1574-148">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your People application.</span><span class="sxs-lookup"><span data-stu-id="a1574-148">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your People application.</span></span>

<span data-ttu-id="a1574-149">**To configure Azure AD SSO with People, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1574-149">**To configure Azure AD SSO with People, perform the following steps:**</span></span>

1. <span data-ttu-id="a1574-150">In the Azure classic portal, on the **People** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="a1574-150">In the Azure classic portal, on the **People** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    <span data-ttu-id="a1574-151">[Configure Single Sign-On][6]</span><span class="sxs-lookup"><span data-stu-id="a1574-151">[Configure Single Sign-On][6]</span></span> 
2. <span data-ttu-id="a1574-152">On the **How would you like users to sign on to People** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-152">On the **How would you like users to sign on to People** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_03.png) 
3. <span data-ttu-id="a1574-154">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="a1574-154">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_04.png) 
   
   1. <span data-ttu-id="a1574-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your People application using the following pattern: **“https://\<company name\>.peoplehr.com/”**.</span><span class="sxs-lookup"><span data-stu-id="a1574-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your People application using the following pattern: **“https://\<company name\>.peoplehr.com/”**.</span></span> 
   2. <span data-ttu-id="a1574-157">If you don't know your tenant URL, contact the People support team via [customerservices@peoplehr.com](mailto:customerservices@peoplehr.com) to get it.</span><span class="sxs-lookup"><span data-stu-id="a1574-157">If you don't know your tenant URL, contact the People support team via [customerservices@peoplehr.com](mailto:customerservices@peoplehr.com) to get it.</span></span>    <span data-ttu-id="a1574-158">3.</span><span class="sxs-lookup"><span data-stu-id="a1574-158">3.</span></span> <span data-ttu-id="a1574-159">In the **Identifier** textbox, type the tenant URL.</span><span class="sxs-lookup"><span data-stu-id="a1574-159">In the **Identifier** textbox, type the tenant URL.</span></span> 
   4. <span data-ttu-id="a1574-160">In the **Reply URL** textbox, type the URL in the following pattern: "**https://itgs.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx**".</span><span class="sxs-lookup"><span data-stu-id="a1574-160">In the **Reply URL** textbox, type the URL in the following pattern: "**https://itgs.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx**".</span></span>
   5. <span data-ttu-id="a1574-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-161">Click **Next**.</span></span>
4. <span data-ttu-id="a1574-162">On the **Configure single sign-on at People** page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="a1574-162">On the **Configure single sign-on at People** page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_05.png) 
   
   1. <span data-ttu-id="a1574-164">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a1574-164">Click **Download metadata**, and then save the file on your computer.</span></span>
   2. <span data-ttu-id="a1574-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-165">Click **Next**.</span></span>
5. <span data-ttu-id="a1574-166">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a1574-166">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
   1. <span data-ttu-id="a1574-167">In the menu on the left side, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a1574-167">In the menu on the left side, click **Settings**.</span></span>
    <span data-ttu-id="a1574-168">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_001.png)</span><span class="sxs-lookup"><span data-stu-id="a1574-168">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_001.png)</span></span>    
   2. <span data-ttu-id="a1574-169">Click **“Company”**.</span><span class="sxs-lookup"><span data-stu-id="a1574-169">Click **“Company”**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_002.png) 
    3. <span data-ttu-id="a1574-171">On the **“Upload 'Single Sign On' SAML meta-data file”**, click **Browse** to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="a1574-171">On the **“Upload 'Single Sign On' SAML meta-data file”**, click **Browse** to upload the downloaded metadata file.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_003.png)
6. <span data-ttu-id="a1574-173">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-173">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="a1574-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a1574-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a1574-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1574-177">Create an Azure AD test user</span></span>
<span data-ttu-id="a1574-178">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1574-178">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

 * <span data-ttu-id="a1574-179">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a1574-179">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="a1574-181">**To create a People test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1574-181">**To create a People test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1574-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1574-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="a1574-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="a1574-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a1574-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a1574-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="a1574-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="a1574-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="a1574-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1574-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="a1574-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="a1574-191">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="a1574-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1574-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="a1574-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-193">Click **Next**.</span></span>
6. <span data-ttu-id="a1574-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1574-194">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="a1574-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a1574-196">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="a1574-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a1574-197">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="a1574-198">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a1574-198">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="a1574-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="a1574-199">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="a1574-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1574-200">Click **Next**.</span></span>
7. <span data-ttu-id="a1574-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="a1574-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="a1574-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1574-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="a1574-205">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="a1574-205">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="a1574-206">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a1574-206">Click **Complete**.</span></span>   

### <a name="create-a-people-test-user"></a><span data-ttu-id="a1574-207">Create a People test user</span><span class="sxs-lookup"><span data-stu-id="a1574-207">Create a People test user</span></span>
<span data-ttu-id="a1574-208">The objective of this section is to create a user called Britta Simon in People.</span><span class="sxs-lookup"><span data-stu-id="a1574-208">The objective of this section is to create a user called Britta Simon in People.</span></span> <span data-ttu-id="a1574-209">People does not support just-in-time provisioning so you need contact the People support team to create an user manually.</span><span class="sxs-lookup"><span data-stu-id="a1574-209">People does not support just-in-time provisioning so you need contact the People support team to create an user manually.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a1574-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1574-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="a1574-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to People.</span><span class="sxs-lookup"><span data-stu-id="a1574-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to People.</span></span>

![Assign User][200] 

<span data-ttu-id="a1574-213">**To assign Britta Simon to People, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1574-213">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="a1574-214">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="a1574-214">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="a1574-216">In the applications list, select **People**.</span><span class="sxs-lookup"><span data-stu-id="a1574-216">In the applications list, select **People**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_people_50.png) 
3. <span data-ttu-id="a1574-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a1574-218">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="a1574-220">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a1574-220">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a1574-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="a1574-221">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a1574-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1574-223">Test single sign-on</span></span>
<span data-ttu-id="a1574-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a1574-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a1574-225">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span><span class="sxs-lookup"><span data-stu-id="a1574-225">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1574-226">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="a1574-226">Additional Resources</span></span>
* [<span data-ttu-id="a1574-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1574-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1574-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1574-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-people-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-people-tutorial/tutorial_general_205.png




























