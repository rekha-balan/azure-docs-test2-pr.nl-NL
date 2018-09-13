---
title: 'Tutorial: Azure Active Directory integration with Fieldglass | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fieldglass.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 596d0db835d9059d11063069527be6435859fdf8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564043"
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="b91f7-103">Tutorial: Azure Active Directory integration with Fieldglass</span><span class="sxs-lookup"><span data-stu-id="b91f7-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>
<span data-ttu-id="b91f7-104">The objective of this tutorial is to show you how to integrate Fieldglass with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b91f7-104">The objective of this tutorial is to show you how to integrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b91f7-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b91f7-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="b91f7-106">You can control in Azure AD who has access to Fieldglass</span><span class="sxs-lookup"><span data-stu-id="b91f7-106">You can control in Azure AD who has access to Fieldglass</span></span>
* <span data-ttu-id="b91f7-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b91f7-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="b91f7-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b91f7-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b91f7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b91f7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b91f7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b91f7-110">Prerequisites</span></span>
<span data-ttu-id="b91f7-111">To configure Azure AD integration with Fieldglass, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b91f7-111">To configure Azure AD integration with Fieldglass, you need the following items:</span></span>

* <span data-ttu-id="b91f7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b91f7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b91f7-113">A Fieldglass single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b91f7-113">A Fieldglass single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b91f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b91f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="b91f7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b91f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b91f7-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b91f7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b91f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b91f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b91f7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b91f7-118">Scenario description</span></span>
<span data-ttu-id="b91f7-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b91f7-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="b91f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b91f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b91f7-121">Adding Fieldglass from the gallery</span><span class="sxs-lookup"><span data-stu-id="b91f7-121">Adding Fieldglass from the gallery</span></span>
2. <span data-ttu-id="b91f7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b91f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-the-gallery"></a><span data-ttu-id="b91f7-123">Adding Fieldglass from the gallery</span><span class="sxs-lookup"><span data-stu-id="b91f7-123">Adding Fieldglass from the gallery</span></span>
<span data-ttu-id="b91f7-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b91f7-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b91f7-125">**To add Fieldglass from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b91f7-125">**To add Fieldglass from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b91f7-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="b91f7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b91f7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b91f7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b91f7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="b91f7-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b91f7-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b91f7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="b91f7-135">In the search box, type **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-135">In the search box, type **Fieldglass**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_01.png)
7. <span data-ttu-id="b91f7-137">In the results pane, select **Fieldglass**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b91f7-137">In the results pane, select **Fieldglass**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_0001.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b91f7-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b91f7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b91f7-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b91f7-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b91f7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="b91f7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass to an user in Azure AD is.</span></span> <span data-ttu-id="b91f7-142">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b91f7-142">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span></span>

<span data-ttu-id="b91f7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="b91f7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fieldglass.</span></span>

<span data-ttu-id="b91f7-144">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b91f7-144">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b91f7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b91f7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b91f7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b91f7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b91f7-147">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b91f7-147">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b91f7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b91f7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b91f7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b91f7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b91f7-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b91f7-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="b91f7-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Fieldglass application.</span><span class="sxs-lookup"><span data-stu-id="b91f7-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="b91f7-152">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b91f7-152">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="b91f7-153">In the classic portal, on the **Fieldglass** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="b91f7-153">In the classic portal, on the **Fieldglass** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="b91f7-155">On the **How would you like users to sign on to Fieldglass** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-155">On the **How would you like users to sign on to Fieldglass** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_03.png) 
3. <span data-ttu-id="b91f7-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="b91f7-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_04.png)
   
    <span data-ttu-id="b91f7-159">a.</span><span class="sxs-lookup"><span data-stu-id="b91f7-159">a.</span></span> <span data-ttu-id="b91f7-160">In the **Identifier** textbox, type URL `https://www.fieldglass.com` or follow the pattern: `https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="b91f7-160">In the **Identifier** textbox, type URL `https://www.fieldglass.com` or follow the pattern: `https://<company name>.fgvms.com`</span></span>
   
    <span data-ttu-id="b91f7-161">b.</span><span class="sxs-lookup"><span data-stu-id="b91f7-161">b.</span></span> <span data-ttu-id="b91f7-162">In the **Reply URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="b91f7-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
   
    - `https://<company name>.fgvms.com/<company name>`
    - `https://www.fieldglass.net/<company name>`
     
    <span data-ttu-id="b91f7-163">c.</span><span class="sxs-lookup"><span data-stu-id="b91f7-163">c.</span></span> <span data-ttu-id="b91f7-164">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="b91f7-164">Click **Next**</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="b91f7-165">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="b91f7-165">Please note that these are not the real values.</span></span> <span data-ttu-id="b91f7-166">You have to update the values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="b91f7-166">You have to update the values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b91f7-167">To get these values, contact [FieldGlass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="b91f7-167">To get these values, contact [FieldGlass](http://www.fieldglass.com/solutions/support).</span></span>
    > 
    >
     
4. <span data-ttu-id="b91f7-168">On the **Configure single sign-on at FieldGlass** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="b91f7-168">On the **Configure single sign-on at FieldGlass** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_05.png)
   
    <span data-ttu-id="b91f7-170">a.</span><span class="sxs-lookup"><span data-stu-id="b91f7-170">a.</span></span> <span data-ttu-id="b91f7-171">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b91f7-171">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="b91f7-172">b.</span><span class="sxs-lookup"><span data-stu-id="b91f7-172">b.</span></span> <span data-ttu-id="b91f7-173">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-173">Click **Next**.</span></span>
5. <span data-ttu-id="b91f7-174">To get SSO configured for your application, contact your Fieldglass support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="b91f7-174">To get SSO configured for your application, contact your Fieldglass support team and provide them with the following:</span></span> 
   
    <span data-ttu-id="b91f7-175">- The **Downloaded certificate** file</span><span class="sxs-lookup"><span data-stu-id="b91f7-175">- The **Downloaded certificate** file</span></span>
   
    <span data-ttu-id="b91f7-176">- The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="b91f7-176">- The **Entity ID**</span></span>
   
    <span data-ttu-id="b91f7-177">- The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="b91f7-177">- The **Single Sign-Out Service URL**</span></span>
6. <span data-ttu-id="b91f7-178">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-178">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="b91f7-180">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-180">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b91f7-182">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b91f7-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="b91f7-183">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b91f7-183">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b91f7-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b91f7-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b91f7-186">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-186">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="b91f7-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b91f7-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b91f7-189">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-189">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="b91f7-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="b91f7-193">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b91f7-193">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_05.png)
   
    <span data-ttu-id="b91f7-195">a.</span><span class="sxs-lookup"><span data-stu-id="b91f7-195">a.</span></span> <span data-ttu-id="b91f7-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b91f7-196">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="b91f7-197">b.</span><span class="sxs-lookup"><span data-stu-id="b91f7-197">b.</span></span> <span data-ttu-id="b91f7-198">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-198">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="b91f7-199">c.</span><span class="sxs-lookup"><span data-stu-id="b91f7-199">c.</span></span> <span data-ttu-id="b91f7-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-200">Click **Next**.</span></span>
6. <span data-ttu-id="b91f7-201">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b91f7-201">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_06.png)
   
    <span data-ttu-id="b91f7-203">a.</span><span class="sxs-lookup"><span data-stu-id="b91f7-203">a.</span></span> <span data-ttu-id="b91f7-204">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-204">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="b91f7-205">b.</span><span class="sxs-lookup"><span data-stu-id="b91f7-205">b.</span></span> <span data-ttu-id="b91f7-206">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-206">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="b91f7-207">c.</span><span class="sxs-lookup"><span data-stu-id="b91f7-207">c.</span></span> <span data-ttu-id="b91f7-208">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-208">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="b91f7-209">d.</span><span class="sxs-lookup"><span data-stu-id="b91f7-209">d.</span></span> <span data-ttu-id="b91f7-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-210">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="b91f7-211">e.</span><span class="sxs-lookup"><span data-stu-id="b91f7-211">e.</span></span> <span data-ttu-id="b91f7-212">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-212">Click **Next**.</span></span>

7. <span data-ttu-id="b91f7-213">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-213">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="b91f7-215">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b91f7-215">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/create_aaduser_08.png)
   
    <span data-ttu-id="b91f7-217">a.</span><span class="sxs-lookup"><span data-stu-id="b91f7-217">a.</span></span> <span data-ttu-id="b91f7-218">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-218">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="b91f7-219">b.</span><span class="sxs-lookup"><span data-stu-id="b91f7-219">b.</span></span> <span data-ttu-id="b91f7-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-220">Click **Complete**.</span></span>   

### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="b91f7-221">Creating a Fieldglass test user</span><span class="sxs-lookup"><span data-stu-id="b91f7-221">Creating a Fieldglass test user</span></span>
<span data-ttu-id="b91f7-222">The objective of this section is to create a user called Britta Simon in FieldGlass.Please work with your Fieldglass support team to add the users in the Fieldglass account.</span><span class="sxs-lookup"><span data-stu-id="b91f7-222">The objective of this section is to create a user called Britta Simon in FieldGlass.Please work with your Fieldglass support team to add the users in the Fieldglass account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b91f7-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b91f7-223">Assigning the Azure AD test user</span></span>
<span data-ttu-id="b91f7-224">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="b91f7-224">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Fieldglass.</span></span>

![Assign User][200]

<span data-ttu-id="b91f7-226">**To assign Britta Simon to Fieldglass, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b91f7-226">**To assign Britta Simon to Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="b91f7-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b91f7-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="b91f7-229">In the applications list, select **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-229">In the applications list, select **Fieldglass**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_50.png)
3. <span data-ttu-id="b91f7-231">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-231">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="b91f7-233">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-233">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b91f7-234">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b91f7-234">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="b91f7-236">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="b91f7-236">Testing single sign-on</span></span>
<span data-ttu-id="b91f7-237">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b91f7-237">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b91f7-238">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span><span class="sxs-lookup"><span data-stu-id="b91f7-238">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b91f7-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b91f7-239">Additional resources</span></span>
* [<span data-ttu-id="b91f7-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b91f7-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b91f7-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b91f7-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fieldglass-tutorial/tutorial_general_205.png

























