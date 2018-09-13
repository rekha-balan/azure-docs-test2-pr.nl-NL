---
title: 'Tutorial: Azure Active Directory integration with Jive | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jive.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: c996327356e4441a965be15af4df4fe02b032be3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661238"
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="d8d77-103">Tutorial: Azure Active Directory integration with Jive</span><span class="sxs-lookup"><span data-stu-id="d8d77-103">Tutorial: Azure Active Directory integration with Jive</span></span>
<span data-ttu-id="d8d77-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8d77-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8d77-105">Integrating Jive with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d8d77-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d8d77-106">You can control in Azure AD who has access to Jive</span><span class="sxs-lookup"><span data-stu-id="d8d77-106">You can control in Azure AD who has access to Jive</span></span>
* <span data-ttu-id="d8d77-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d8d77-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="d8d77-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d8d77-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d8d77-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8d77-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8d77-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8d77-110">Prerequisites</span></span>
<span data-ttu-id="d8d77-111">To configure Azure AD integration with Jive, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d8d77-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

* <span data-ttu-id="d8d77-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d8d77-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d8d77-113">A Jive single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d8d77-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8d77-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d8d77-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="d8d77-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d8d77-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d8d77-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d8d77-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d8d77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8d77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8d77-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="d8d77-118">Scenario Description</span></span>
<span data-ttu-id="d8d77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d8d77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="d8d77-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8d77-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8d77-121">Adding Jive from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8d77-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="d8d77-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8d77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="d8d77-123">Adding Jive from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8d77-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="d8d77-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d8d77-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8d77-125">**To add Jive from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8d77-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d77-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="d8d77-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d8d77-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d8d77-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d8d77-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d8d77-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d8d77-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d8d77-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d8d77-135">In the search box, type **Jive**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-135">In the search box, type **Jive**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_01.png)
7. <span data-ttu-id="d8d77-137">In the results pane, select **Jive**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d8d77-137">In the results pane, select **Jive**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8d77-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8d77-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8d77-140">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d8d77-140">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8d77-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8d77-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="d8d77-142">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d8d77-142">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="d8d77-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="d8d77-144">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8d77-144">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8d77-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d8d77-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8d77-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8d77-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8d77-147">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d8d77-147">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d8d77-148">**[Configuring user provisioning](#configuring-user-provisioning)** - to outline how to enable user provisioning of Active Directory user accounts to Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-148">**[Configuring user provisioning](#configuring-user-provisioning)** - to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
5. <span data-ttu-id="d8d77-149">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d8d77-149">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="d8d77-150">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d8d77-150">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8d77-151">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8d77-151">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="d8d77-152">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Jive application.</span><span class="sxs-lookup"><span data-stu-id="d8d77-152">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="d8d77-153">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8d77-153">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d77-154">In the classic portal, on the **Jive** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d8d77-154">In the classic portal, on the **Jive** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="d8d77-156">On the **How would you like users to sign on to Jive** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-156">On the **How would you like users to sign on to Jive** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_03.png) 
3. <span data-ttu-id="d8d77-158">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8d77-158">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_04.png) 
   
    <span data-ttu-id="d8d77-160">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-160">a.</span></span> <span data-ttu-id="d8d77-161">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Jive application using the following pattern: **https://\<customer name\>.jivecustom.com**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-161">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Jive application using the following pattern: **https://\<customer name\>.jivecustom.com**.</span></span>
   
    <span data-ttu-id="d8d77-162">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-162">b.</span></span> <span data-ttu-id="d8d77-163">click **Next**</span><span class="sxs-lookup"><span data-stu-id="d8d77-163">click **Next**</span></span>
4. <span data-ttu-id="d8d77-164">On the **Configure single sign-on at Jive** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8d77-164">On the **Configure single sign-on at Jive** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_05.png)
   
    <span data-ttu-id="d8d77-166">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-166">a.</span></span> <span data-ttu-id="d8d77-167">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d8d77-167">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="d8d77-168">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-168">b.</span></span> <span data-ttu-id="d8d77-169">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-169">Click **Next**.</span></span>
5. <span data-ttu-id="d8d77-170">Sign-on to your Jive tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d8d77-170">Sign-on to your Jive tenant as an administrator.</span></span>
6. <span data-ttu-id="d8d77-171">In the menu on the top, Click "**Saml**".</span><span class="sxs-lookup"><span data-stu-id="d8d77-171">In the menu on the top, Click "**Saml**".</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)
   
    <span data-ttu-id="d8d77-173">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-173">a.</span></span> <span data-ttu-id="d8d77-174">Select **Enabled** under the **Genaral** tab.</span><span class="sxs-lookup"><span data-stu-id="d8d77-174">Select **Enabled** under the **Genaral** tab.</span></span>
   
    <span data-ttu-id="d8d77-175">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-175">b.</span></span> <span data-ttu-id="d8d77-176">Click the "**Save all saml settings**" button.</span><span class="sxs-lookup"><span data-stu-id="d8d77-176">Click the "**Save all saml settings**" button.</span></span>
7. <span data-ttu-id="d8d77-177">Navigate to the "**Idp Metadata**" tab.</span><span class="sxs-lookup"><span data-stu-id="d8d77-177">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="d8d77-179">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-179">a.</span></span> <span data-ttu-id="d8d77-180">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="d8d77-180">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
   
    <span data-ttu-id="d8d77-181">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-181">b.</span></span> <span data-ttu-id="d8d77-182">Click the "**Save all saml settings**" button.</span><span class="sxs-lookup"><span data-stu-id="d8d77-182">Click the "**Save all saml settings**" button.</span></span> 
8. <span data-ttu-id="d8d77-183">Go to the "**User Attribute Mapping**" tab.</span><span class="sxs-lookup"><span data-stu-id="d8d77-183">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="d8d77-185">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-185">a.</span></span> <span data-ttu-id="d8d77-186">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span><span class="sxs-lookup"><span data-stu-id="d8d77-186">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="d8d77-187">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-187">b.</span></span> <span data-ttu-id="d8d77-188">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span><span class="sxs-lookup"><span data-stu-id="d8d77-188">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="d8d77-189">c.</span><span class="sxs-lookup"><span data-stu-id="d8d77-189">c.</span></span> <span data-ttu-id="d8d77-190">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span><span class="sxs-lookup"><span data-stu-id="d8d77-190">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>
9. <span data-ttu-id="d8d77-191">In the Azure AD portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-191">In the Azure AD portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   <span data-ttu-id="d8d77-192">![Azure AD Single Sign-On][10]</span><span class="sxs-lookup"><span data-stu-id="d8d77-192">![Azure AD Single Sign-On][10]</span></span>
10. <span data-ttu-id="d8d77-193">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-193">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    <span data-ttu-id="d8d77-194">![Azure AD Single Sign-On][11]</span><span class="sxs-lookup"><span data-stu-id="d8d77-194">![Azure AD Single Sign-On][11]</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8d77-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8d77-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8d77-196">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8d77-196">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d8d77-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8d77-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d77-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="d8d77-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d8d77-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d8d77-202">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d8d77-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="d8d77-206">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="d8d77-206">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_05.png)</span></span> 
   
    <span data-ttu-id="d8d77-207">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-207">a.</span></span> <span data-ttu-id="d8d77-208">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d8d77-208">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="d8d77-209">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-209">b.</span></span> <span data-ttu-id="d8d77-210">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-210">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="d8d77-211">c.</span><span class="sxs-lookup"><span data-stu-id="d8d77-211">c.</span></span> <span data-ttu-id="d8d77-212">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-212">Click **Next**.</span></span>
6. <span data-ttu-id="d8d77-213">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8d77-213">On the **User Profile** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="d8d77-215">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-215">a.</span></span> <span data-ttu-id="d8d77-216">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-216">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="d8d77-217">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-217">b.</span></span> <span data-ttu-id="d8d77-218">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-218">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="d8d77-219">c.</span><span class="sxs-lookup"><span data-stu-id="d8d77-219">c.</span></span> <span data-ttu-id="d8d77-220">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-220">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="d8d77-221">d.</span><span class="sxs-lookup"><span data-stu-id="d8d77-221">d.</span></span> <span data-ttu-id="d8d77-222">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-222">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="d8d77-223">e.</span><span class="sxs-lookup"><span data-stu-id="d8d77-223">e.</span></span> <span data-ttu-id="d8d77-224">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-224">Click **Next**.</span></span>
7. <span data-ttu-id="d8d77-225">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-225">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d8d77-227">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8d77-227">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="d8d77-229">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-229">a.</span></span> <span data-ttu-id="d8d77-230">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-230">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="d8d77-231">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-231">b.</span></span> <span data-ttu-id="d8d77-232">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-232">Click **Complete**.</span></span>   

### <a name="creating-a-jive-test-user"></a><span data-ttu-id="d8d77-233">Creating a Jive test user</span><span class="sxs-lookup"><span data-stu-id="d8d77-233">Creating a Jive test user</span></span>
<span data-ttu-id="d8d77-234">In this section, you create a user called Britta Simon in Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-234">In this section, you create a user called Britta Simon in Jive.</span></span> <span data-ttu-id="d8d77-235">Please work with Jive support team to add the users in the Jive platform.</span><span class="sxs-lookup"><span data-stu-id="d8d77-235">Please work with Jive support team to add the users in the Jive platform.</span></span>

### <a name="configuring-user-provisioning"></a><span data-ttu-id="d8d77-236">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="d8d77-236">Configuring user provisioning</span></span>
<span data-ttu-id="d8d77-237">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-237">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>  
<span data-ttu-id="d8d77-238">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span><span class="sxs-lookup"><span data-stu-id="d8d77-238">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

<span data-ttu-id="d8d77-239">The following screenshot shows an example of the related dialog in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d8d77-239">The following screenshot shows an example of the related dialog in Azure AD:</span></span>

<span data-ttu-id="d8d77-240">![Configure User Provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/IC698794.png "Configure User Provisioning")</span><span class="sxs-lookup"><span data-stu-id="d8d77-240">![Configure User Provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/IC698794.png "Configure User Provisioning")</span></span>

#### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="d8d77-241">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8d77-241">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="d8d77-242">In the Azure Management Portal, on the **Jive** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span><span class="sxs-lookup"><span data-stu-id="d8d77-242">In the Azure Management Portal, on the **Jive** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
2. <span data-ttu-id="d8d77-243">On the **Enter your Jive credentials to enable automatic user provisioning** page, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="d8d77-243">On the **Enter your Jive credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="d8d77-244">a.</span><span class="sxs-lookup"><span data-stu-id="d8d77-244">a.</span></span> <span data-ttu-id="d8d77-245">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span><span class="sxs-lookup"><span data-stu-id="d8d77-245">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="d8d77-246">b.</span><span class="sxs-lookup"><span data-stu-id="d8d77-246">b.</span></span> <span data-ttu-id="d8d77-247">In the **Jive Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="d8d77-247">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="d8d77-248">c.</span><span class="sxs-lookup"><span data-stu-id="d8d77-248">c.</span></span> <span data-ttu-id="d8d77-249">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span><span class="sxs-lookup"><span data-stu-id="d8d77-249">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="d8d77-250">The Jive tenant URL is URL that is used by your organization to log into Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-250">The Jive tenant URL is URL that is used by your organization to log into Jive.</span></span>  
      > <span data-ttu-id="d8d77-251">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-251">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>
      > 
      > 
   
    <span data-ttu-id="d8d77-252">d.</span><span class="sxs-lookup"><span data-stu-id="d8d77-252">d.</span></span> <span data-ttu-id="d8d77-253">Click **validate** to verify your configuration.</span><span class="sxs-lookup"><span data-stu-id="d8d77-253">Click **validate** to verify your configuration.</span></span>

    <span data-ttu-id="d8d77-254">e.</span><span class="sxs-lookup"><span data-stu-id="d8d77-254">e.</span></span> <span data-ttu-id="d8d77-255">Click the **Next** button to open the **Confirmation** page.</span><span class="sxs-lookup"><span data-stu-id="d8d77-255">Click the **Next** button to open the **Confirmation** page.</span></span>

3. <span data-ttu-id="d8d77-256">On the **Confirmation** page, click the checkmark to save your configuration.</span><span class="sxs-lookup"><span data-stu-id="d8d77-256">On the **Confirmation** page, click the checkmark to save your configuration.</span></span>

<span data-ttu-id="d8d77-257">You can now create a test account, wait for 10 minutes and verify that the account has been synchronized to Jive.com.</span><span class="sxs-lookup"><span data-stu-id="d8d77-257">You can now create a test account, wait for 10 minutes and verify that the account has been synchronized to Jive.com.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d8d77-258">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8d77-258">Assigning the Azure AD test user</span></span>
<span data-ttu-id="d8d77-259">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Jive.</span><span class="sxs-lookup"><span data-stu-id="d8d77-259">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Jive.</span></span>

![Assign User][200] 

<span data-ttu-id="d8d77-261">**To assign Britta Simon to Jive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8d77-261">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d77-262">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d8d77-262">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="d8d77-264">In the applications list, select **Jive**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-264">In the applications list, select **Jive**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_jive_50.png) 
3. <span data-ttu-id="d8d77-266">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-266">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="d8d77-268">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-268">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d8d77-269">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d8d77-269">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="d8d77-271">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8d77-271">Testing Single Sign-On</span></span>
<span data-ttu-id="d8d77-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d8d77-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d8d77-273">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span><span class="sxs-lookup"><span data-stu-id="d8d77-273">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8d77-274">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="d8d77-274">Additional Resources</span></span>
* [<span data-ttu-id="d8d77-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8d77-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8d77-276">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8d77-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-jive-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-jive-tutorial/tutorial_general_205.png





























