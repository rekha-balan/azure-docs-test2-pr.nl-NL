---
title: 'Tutorial: Azure Active Directory integration with Showpad | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Showpad.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3746a77668e4a2ac07afe7f506787c519f8f5543
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551083"
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="1eb7d-103">Tutorial: Azure Active Directory integration with Showpad</span><span class="sxs-lookup"><span data-stu-id="1eb7d-103">Tutorial: Azure Active Directory integration with Showpad</span></span>
<span data-ttu-id="1eb7d-104">The objective of this tutorial is to show you how to integrate Showpad with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1eb7d-104">The objective of this tutorial is to show you how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eb7d-105">Integrating Showpad with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1eb7d-106">You can control in Azure AD who has access to Showpad</span><span class="sxs-lookup"><span data-stu-id="1eb7d-106">You can control in Azure AD who has access to Showpad</span></span>
* <span data-ttu-id="1eb7d-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1eb7d-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="1eb7d-108">You can manage your accounts in one central location - the Azure Active Directory Portal</span><span class="sxs-lookup"><span data-stu-id="1eb7d-108">You can manage your accounts in one central location - the Azure Active Directory Portal</span></span>

<span data-ttu-id="1eb7d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1eb7d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eb7d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1eb7d-110">Prerequisites</span></span>
<span data-ttu-id="1eb7d-111">To configure Azure AD integration with Showpad, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

* <span data-ttu-id="1eb7d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1eb7d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1eb7d-113">A Showpad subscription</span><span class="sxs-lookup"><span data-stu-id="1eb7d-113">A Showpad subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1eb7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1eb7d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1eb7d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1eb7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1eb7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eb7d-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="1eb7d-118">Scenario Description</span></span>
<span data-ttu-id="1eb7d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="1eb7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eb7d-121">Adding Showpad from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eb7d-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="1eb7d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eb7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="1eb7d-123">Adding Showpad from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eb7d-123">Adding Showpad from the gallery</span></span>
<span data-ttu-id="1eb7d-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1eb7d-125">**To add Showpad from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb7d-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb7d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Applications][1]

2. <span data-ttu-id="1eb7d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1eb7d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="1eb7d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="1eb7d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="1eb7d-135">In the search box, type **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-135">In the search box, type **Showpad**.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_01.png)

7. <span data-ttu-id="1eb7d-137">In the results pane, select **Showpad**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-137">In the results pane, select **Showpad**, and then click **Complete** to add the application.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1eb7d-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eb7d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1eb7d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1eb7d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1eb7d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad to an user in Azure AD is.</span></span> <span data-ttu-id="1eb7d-142">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-142">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="1eb7d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Showpad.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Showpad.</span></span>

<span data-ttu-id="1eb7d-144">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-144">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1eb7d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1eb7d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eb7d-147">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-147">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1eb7d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eb7d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1eb7d-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1eb7d-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="1eb7d-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Showpad application.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="1eb7d-152">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb7d-152">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb7d-153">In the Azure classic portal, on the **Showpad** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-153">In the Azure classic portal, on the **Showpad** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="1eb7d-155">On the **How would you like users to sign on to Showpad** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-155">On the **How would you like users to sign on to Showpad** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_03.png)

3. <span data-ttu-id="1eb7d-157">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-157">On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_04.png) 

    <span data-ttu-id="1eb7d-159">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-159">a.</span></span> <span data-ttu-id="1eb7d-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Showpad application using the following pattern: `https://<company name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="1eb7d-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Showpad application using the following pattern: `https://<company name>.showpad.biz/login`</span></span>

    <span data-ttu-id="1eb7d-161">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-161">b.</span></span> <span data-ttu-id="1eb7d-162">In the **Identifier** textbox, type the URL using the following pattern: `https://<company name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="1eb7d-162">In the **Identifier** textbox, type the URL using the following pattern: `https://<company name>.showpad.biz`</span></span>

    <span data-ttu-id="1eb7d-163">c.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-163">c.</span></span> <span data-ttu-id="1eb7d-164">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="1eb7d-164">Click **Next**</span></span>


1. <span data-ttu-id="1eb7d-165">On the **Configure single sign-on at Showpad** page, perform the following steps and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-165">On the **Configure single sign-on at Showpad** page, perform the following steps and then click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_05.png)
   
    <span data-ttu-id="1eb7d-167">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-167">a.</span></span> <span data-ttu-id="1eb7d-168">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-168">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="1eb7d-169">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-169">b.</span></span> <span data-ttu-id="1eb7d-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-170">Click **Next**.</span></span>

2. <span data-ttu-id="1eb7d-171">Sign-on to your Showpad tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-171">Sign-on to your Showpad tenant as an administrator.</span></span>

3. <span data-ttu-id="1eb7d-172">In the menu on the top, click the **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-172">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

4. <span data-ttu-id="1eb7d-174">Navigate to "**Single Sign-On**" and click "**Enable**".</span><span class="sxs-lookup"><span data-stu-id="1eb7d-174">Navigate to "**Single Sign-On**" and click "**Enable**".</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

5. <span data-ttu-id="1eb7d-176">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-176">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="1eb7d-178">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-178">a.</span></span> <span data-ttu-id="1eb7d-179">In the **Name** textbox, type the name of Identifier Provider (e.g.: your company name).</span><span class="sxs-lookup"><span data-stu-id="1eb7d-179">In the **Name** textbox, type the name of Identifier Provider (e.g.: your company name).</span></span>
   
    <span data-ttu-id="1eb7d-180">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-180">b.</span></span> <span data-ttu-id="1eb7d-181">As **Metadata Source**, select **XML**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-181">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="1eb7d-182">c.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-182">c.</span></span> <span data-ttu-id="1eb7d-183">Copy the content of the downloaded metadata XML file, and then paste it into the **Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-183">Copy the content of the downloaded metadata XML file, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="1eb7d-184">d.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-184">d.</span></span> <span data-ttu-id="1eb7d-185">Select **Auto-provision accounts for new users when they log in**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-185">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="1eb7d-186">e.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-186">e.</span></span> <span data-ttu-id="1eb7d-187">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-187">Click **Submit**.</span></span>

6. <span data-ttu-id="1eb7d-188">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-188">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="1eb7d-190">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-190">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1eb7d-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eb7d-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1eb7d-193">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-193">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1eb7d-195">**To create a Showpad test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb7d-195">**To create a Showpad test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb7d-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1eb7d-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1eb7d-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-199">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1eb7d-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1eb7d-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="1eb7d-205">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-205">a.</span></span> <span data-ttu-id="1eb7d-206">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-206">In the **User Name** textbox, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="1eb7d-207">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-207">b.</span></span> <span data-ttu-id="1eb7d-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-208">Click **Next**.</span></span>

6. <span data-ttu-id="1eb7d-209">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-209">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="1eb7d-211">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-211">a.</span></span> <span data-ttu-id="1eb7d-212">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-212">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="1eb7d-213">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-213">b.</span></span> <span data-ttu-id="1eb7d-214">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-214">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="1eb7d-215">c.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-215">c.</span></span> <span data-ttu-id="1eb7d-216">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-216">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="1eb7d-217">d.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-217">d.</span></span> <span data-ttu-id="1eb7d-218">As **Role**, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-218">As **Role**, select **User**.</span></span>
   
    <span data-ttu-id="1eb7d-219">e.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-219">e.</span></span> <span data-ttu-id="1eb7d-220">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-220">Click **Next**.</span></span>

7. <span data-ttu-id="1eb7d-221">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-221">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_07.png)

8. <span data-ttu-id="1eb7d-223">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eb7d-223">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="1eb7d-225">a.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-225">a.</span></span> <span data-ttu-id="1eb7d-226">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-226">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="1eb7d-227">b.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-227">b.</span></span> <span data-ttu-id="1eb7d-228">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-228">Click **Complete**.</span></span>

### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="1eb7d-229">Creating a Showpad test user</span><span class="sxs-lookup"><span data-stu-id="1eb7d-229">Creating a Showpad test user</span></span>
<span data-ttu-id="1eb7d-230">The objective of this section is to create a user called Britta Simon in Showpad.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-230">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="1eb7d-231">Showpad supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-231">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="1eb7d-232">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-232">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**.</span></span> 

<span data-ttu-id="1eb7d-233">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-233">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1eb7d-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eb7d-234">Assigning the Azure AD test user</span></span>
<span data-ttu-id="1eb7d-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Showpad.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Showpad.</span></span>

![Assign User][200]

<span data-ttu-id="1eb7d-237">**To assign Britta Simon to Showpad, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eb7d-237">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb7d-238">On the Azure classic portal, in the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-238">On the Azure classic portal, in the menu on the top, click **Applications**.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="1eb7d-240">In the applications list, click **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-240">In the applications list, click **Showpad**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_showpad_50.png) 
3. <span data-ttu-id="1eb7d-242">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-242">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="1eb7d-244">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-244">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1eb7d-245">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-245">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="1eb7d-247">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1eb7d-247">Testing Single Sign-On</span></span>
<span data-ttu-id="1eb7d-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1eb7d-249">When you click the **Showpad** tile in the Access Panel, you should get automatically signed-on to your Showpad application.</span><span class="sxs-lookup"><span data-stu-id="1eb7d-249">When you click the **Showpad** tile in the Access Panel, you should get automatically signed-on to your Showpad application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1eb7d-250">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="1eb7d-250">Additional Resources</span></span>
* [<span data-ttu-id="1eb7d-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eb7d-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eb7d-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1eb7d-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-showpad-tutorial/tutorial_general_205.png




























