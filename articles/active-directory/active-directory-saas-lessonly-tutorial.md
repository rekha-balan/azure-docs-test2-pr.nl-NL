---
title: 'Tutorial: Azure Active Directory integration with Lesson.ly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lesson.ly.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 81bb6dce1c9b8c314424caf32b94683a0956f65d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548736"
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="4ed5d-103">Tutorial: Azure Active Directory integration with Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="4ed5d-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>
<span data-ttu-id="4ed5d-104">The objective of this tutorial is to show you how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ed5d-104">The objective of this tutorial is to show you how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ed5d-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4ed5d-106">You can control in Azure AD who has access to Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="4ed5d-106">You can control in Azure AD who has access to Lesson.ly</span></span>
* <span data-ttu-id="4ed5d-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4ed5d-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="4ed5d-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4ed5d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4ed5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ed5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ed5d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ed5d-110">Prerequisites</span></span>
<span data-ttu-id="4ed5d-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

* <span data-ttu-id="4ed5d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4ed5d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4ed5d-113">A Lesson.ly single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4ed5d-113">A Lesson.ly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ed5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="4ed5d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4ed5d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4ed5d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ed5d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ed5d-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="4ed5d-118">Scenario Description</span></span>
<span data-ttu-id="4ed5d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="4ed5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ed5d-121">Adding Lesson.ly from the gallery</span><span class="sxs-lookup"><span data-stu-id="4ed5d-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="4ed5d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4ed5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="4ed5d-123">Adding Lesson.ly from the gallery</span><span class="sxs-lookup"><span data-stu-id="4ed5d-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="4ed5d-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4ed5d-125">**To add Lesson.ly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4ed5d-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed5d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="4ed5d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4ed5d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="4ed5d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="4ed5d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="4ed5d-135">In the search box, type **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-135">In the search box, type **Lesson.ly**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_01.png)
7. <span data-ttu-id="4ed5d-137">In the results pane, select **Lesson.ly**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-137">In the results pane, select **Lesson.ly**, and then click **Complete** to add the application.</span></span>

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ed5d-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4ed5d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ed5d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ed5d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ed5d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly to an user in Azure AD is.</span></span> <span data-ttu-id="4ed5d-142">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-142">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="4ed5d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lesson.ly.</span></span>

<span data-ttu-id="4ed5d-144">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-144">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4ed5d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4ed5d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ed5d-147">**[Creating a Lesson.ly test user](#creating-a-Lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-147">**[Creating a Lesson.ly test user](#creating-a-Lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4ed5d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ed5d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ed5d-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ed5d-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="4ed5d-151">The objective of this section is to outline how to enable users to authenticate to Lesson.ly with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-151">The objective of this section is to outline how to enable users to authenticate to Lesson.ly with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="4ed5d-152">Your Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-152">Your Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>
<span data-ttu-id="4ed5d-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-153">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png) 

<span data-ttu-id="4ed5d-155">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4ed5d-155">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed5d-156">In the Azure classic portal, on the Lesson.ly application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-156">In the Azure classic portal, on the Lesson.ly application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_07.png) 
2. <span data-ttu-id="4ed5d-158">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-158">To add the required attribute mappings, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_08.png) 
   
    <span data-ttu-id="4ed5d-160">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-160">a.</span></span> <span data-ttu-id="4ed5d-161">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-161">For each data row in the table above, click **add user attribute**.</span></span>
   
    <span data-ttu-id="4ed5d-162">b.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-162">b.</span></span> <span data-ttu-id="4ed5d-163">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-163">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   
    <span data-ttu-id="4ed5d-164">c.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-164">c.</span></span> <span data-ttu-id="4ed5d-165">From the **Attribute Value** list, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-165">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
   
    <span data-ttu-id="4ed5d-166">d.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-166">d.</span></span> <span data-ttu-id="4ed5d-167">Click **Complete**</span><span class="sxs-lookup"><span data-stu-id="4ed5d-167">Click **Complete**</span></span>
3. <span data-ttu-id="4ed5d-168">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-168">Click **Apply Changes**.</span></span>
4. <span data-ttu-id="4ed5d-169">In your browser, click **Back** to open the Quick Start dialog again</span><span class="sxs-lookup"><span data-stu-id="4ed5d-169">In your browser, click **Back** to open the Quick Start dialog again</span></span>
5. <span data-ttu-id="4ed5d-170">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-170">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
6. <span data-ttu-id="4ed5d-172">On the **How would you like users to sign on to Lesson.ly** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-172">On the **How would you like users to sign on to Lesson.ly** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_03.png) 
7. <span data-ttu-id="4ed5d-174">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-174">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_04.png) 

    <span data-ttu-id="4ed5d-176">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-176">a.</span></span> <span data-ttu-id="4ed5d-177">In the Sign On URL textbox, type the URL used by your users to sign-on to your Lessonly application using the following pattern: **“https://companyname.lesson.ly/signin”**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-177">In the Sign On URL textbox, type the URL used by your users to sign-on to your Lessonly application using the following pattern: **“https://companyname.lesson.ly/signin”**.</span></span> <span data-ttu-id="4ed5d-178">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-178">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>


1. <span data-ttu-id="4ed5d-179">On the **Configure single sign-on at Lesson.ly** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-179">On the **Configure single sign-on at Lesson.ly** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_05.png) 
   
    <span data-ttu-id="4ed5d-181">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-181">a.</span></span> <span data-ttu-id="4ed5d-182">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-182">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="4ed5d-183">b.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-183">b.</span></span> <span data-ttu-id="4ed5d-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-184">Click **Next**.</span></span>
2. <span data-ttu-id="4ed5d-185">To get SSO configured for your application, contact your Lesson.ly support team via dev@lessonly.com.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-185">To get SSO configured for your application, contact your Lesson.ly support team via dev@lessonly.com.</span></span> <span data-ttu-id="4ed5d-186">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Lesson.ly team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-186">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Lesson.ly team to set up SSO on their side.</span></span>
3. <span data-ttu-id="4ed5d-187">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-187">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
   ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="4ed5d-189">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-189">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
   ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ed5d-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4ed5d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ed5d-192">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-192">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="4ed5d-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4ed5d-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed5d-195">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-195">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="4ed5d-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4ed5d-198">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-198">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="4ed5d-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="4ed5d-202">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-202">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="4ed5d-204">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-204">a.</span></span> <span data-ttu-id="4ed5d-205">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-205">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="4ed5d-206">b.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-206">b.</span></span> <span data-ttu-id="4ed5d-207">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-207">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="4ed5d-208">c.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-208">c.</span></span> <span data-ttu-id="4ed5d-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-209">Click **Next**.</span></span>
6. <span data-ttu-id="4ed5d-210">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-210">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="4ed5d-212">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-212">a.</span></span> <span data-ttu-id="4ed5d-213">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-213">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="4ed5d-214">b.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-214">b.</span></span> <span data-ttu-id="4ed5d-215">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-215">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="4ed5d-216">c.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-216">c.</span></span> <span data-ttu-id="4ed5d-217">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-217">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="4ed5d-218">d.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-218">d.</span></span> <span data-ttu-id="4ed5d-219">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-219">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="4ed5d-220">e.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-220">e.</span></span> <span data-ttu-id="4ed5d-221">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-221">Click **Next**.</span></span>

7. <span data-ttu-id="4ed5d-222">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-222">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="4ed5d-224">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4ed5d-224">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="4ed5d-226">a.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-226">a.</span></span> <span data-ttu-id="4ed5d-227">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-227">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="4ed5d-228">b.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-228">b.</span></span> <span data-ttu-id="4ed5d-229">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-229">Click **Complete**.</span></span>   

### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="4ed5d-230">Creating a Lesson.ly test user</span><span class="sxs-lookup"><span data-stu-id="4ed5d-230">Creating a Lesson.ly test user</span></span>
<span data-ttu-id="4ed5d-231">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-231">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="4ed5d-232">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-232">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4ed5d-233">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-233">There is no action item for you in this section.</span></span> <span data-ttu-id="4ed5d-234">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-234">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span> <span data-ttu-id="4ed5d-235">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4ed5d-235">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

> [!NOTE]
> <span data-ttu-id="4ed5d-236">If you need to create an user manually, you need to contact the Lesson.ly support team.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-236">If you need to create an user manually, you need to contact the Lesson.ly support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4ed5d-237">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4ed5d-237">Assigning the Azure AD test user</span></span>
<span data-ttu-id="4ed5d-238">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-238">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Lesson.ly.</span></span>

![Assign User][200] 

<span data-ttu-id="4ed5d-240">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4ed5d-240">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed5d-241">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-241">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="4ed5d-243">In the applications list, select **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-243">In the applications list, select **Lesson.ly**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_50.png) 
3. <span data-ttu-id="4ed5d-245">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-245">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="4ed5d-247">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-247">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="4ed5d-248">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-248">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="4ed5d-250">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ed5d-250">Testing Single Sign-On</span></span>
<span data-ttu-id="4ed5d-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4ed5d-252">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span><span class="sxs-lookup"><span data-stu-id="4ed5d-252">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ed5d-253">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="4ed5d-253">Additional Resources</span></span>
* [<span data-ttu-id="4ed5d-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ed5d-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ed5d-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ed5d-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lessonly-tutorial/tutorial_general_205.png




























