---
title: 'Tutorial: Azure Active Directory integration with Pluralsight | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pluralsight.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: e2b3b3000a89253a23141ec1164fb6fb279f6d5c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553829"
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="28568-103">Tutorial: Azure Active Directory integration with Pluralsight</span><span class="sxs-lookup"><span data-stu-id="28568-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>
<span data-ttu-id="28568-104">The objective of this tutorial is to show you how to integrate Pluralsight with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28568-104">The objective of this tutorial is to show you how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28568-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="28568-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="28568-106">You can control in Azure AD who has access to Pluralsight</span><span class="sxs-lookup"><span data-stu-id="28568-106">You can control in Azure AD who has access to Pluralsight</span></span>
* <span data-ttu-id="28568-107">You can enable your users to automatically get signed-on to Pluralsight single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="28568-107">You can enable your users to automatically get signed-on to Pluralsight single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="28568-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="28568-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="28568-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28568-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28568-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="28568-110">Prerequisites</span></span>
<span data-ttu-id="28568-111">To configure Azure AD integration with Pluralsight, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="28568-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

* <span data-ttu-id="28568-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="28568-112">An Azure subscription</span></span>
* <span data-ttu-id="28568-113">A Pluralsight SSO on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="28568-113">A Pluralsight SSO on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="28568-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="28568-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="28568-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="28568-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="28568-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="28568-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="28568-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28568-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28568-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="28568-118">Scenario Description</span></span>
<span data-ttu-id="28568-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="28568-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="28568-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="28568-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28568-121">Adding Pluralsight from the gallery</span><span class="sxs-lookup"><span data-stu-id="28568-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="28568-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="28568-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-pluralsight-from-the-gallery"></a><span data-ttu-id="28568-123">Add Pluralsight from the gallery</span><span class="sxs-lookup"><span data-stu-id="28568-123">Add Pluralsight from the gallery</span></span>
<span data-ttu-id="28568-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="28568-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28568-125">**To add Pluralsight from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="28568-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28568-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28568-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="28568-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="28568-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="28568-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="28568-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="28568-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="28568-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="28568-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="28568-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="28568-135">In the search box, type **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="28568-135">In the search box, type **Pluralsight**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_01.png)
7. <span data-ttu-id="28568-137">In the results pane, select **Pluralsight**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="28568-137">In the results pane, select **Pluralsight**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="28568-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="28568-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="28568-140">The objective of this section is to show you how to configure and test Azure AD SSO with Pluralsight based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="28568-140">The objective of this section is to show you how to configure and test Azure AD SSO with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28568-141">To configure and test Azure AD SSO with Pluralsight, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="28568-141">To configure and test Azure AD SSO with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28568-142">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="28568-142">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28568-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28568-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28568-144">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="28568-144">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="28568-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="28568-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28568-146">**[Testing Single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="28568-146">**[Testing Single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="28568-147">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="28568-147">Configure Azure AD SSO</span></span>
<span data-ttu-id="28568-148">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="28568-148">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Pluralsight application.</span></span>

<span data-ttu-id="28568-149">Your Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="28568-149">Your Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="28568-150">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="28568-150">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_02.png) 

<span data-ttu-id="28568-152">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span><span class="sxs-lookup"><span data-stu-id="28568-152">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="28568-153">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span><span class="sxs-lookup"><span data-stu-id="28568-153">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

<span data-ttu-id="28568-154">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="28568-154">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="28568-155">In the Azure classic portal, on the **Pluralsight** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="28568-155">In the Azure classic portal, on the **Pluralsight** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_81.png) 
2. <span data-ttu-id="28568-157">To remove the redundant **SAML token attributes**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-157">To remove the redundant **SAML token attributes**, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/2829.png) 
  * <span data-ttu-id="28568-159">For each user attribute in the red box of the table above, hover over the attribute, and then click delete.</span><span class="sxs-lookup"><span data-stu-id="28568-159">For each user attribute in the red box of the table above, hover over the attribute, and then click delete.</span></span> 
3. <span data-ttu-id="28568-160">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-160">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="28568-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="28568-161">Attribute Name</span></span> | <span data-ttu-id="28568-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="28568-162">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="28568-163">First Name</span><span class="sxs-lookup"><span data-stu-id="28568-163">First Name</span></span> |<span data-ttu-id="28568-164">user.givenname</span><span class="sxs-lookup"><span data-stu-id="28568-164">user.givenname</span></span> |
   | <span data-ttu-id="28568-165">Last Name</span><span class="sxs-lookup"><span data-stu-id="28568-165">Last Name</span></span> |<span data-ttu-id="28568-166">user.surname</span><span class="sxs-lookup"><span data-stu-id="28568-166">user.surname</span></span> |
   | <span data-ttu-id="28568-167">Email</span><span class="sxs-lookup"><span data-stu-id="28568-167">Email</span></span> |<span data-ttu-id="28568-168">user.mail</span><span class="sxs-lookup"><span data-stu-id="28568-168">user.mail</span></span> |
4. <span data-ttu-id="28568-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="28568-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_82.png)
  1. <span data-ttu-id="28568-171">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="28568-171">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
  2. <span data-ttu-id="28568-172">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="28568-172">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
  3. <span data-ttu-id="28568-173">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="28568-173">Click **Complete**.</span></span>    
  4. <span data-ttu-id="28568-174">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="28568-174">Click **Apply Changes**.</span></span>
 
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/3232.png) 
    
5. <span data-ttu-id="28568-176">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="28568-176">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_83.png)  
6. <span data-ttu-id="28568-178">In the Azure classic portal, on the **Pluralsight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="28568-178">In the Azure classic portal, on the **Pluralsight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
7. <span data-ttu-id="28568-180">On the **How would you like users to sign on to Pluralsight** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-180">On the **How would you like users to sign on to Pluralsight** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_03.png) 
8. <span data-ttu-id="28568-182">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="28568-182">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_04.png) 
  1. <span data-ttu-id="28568-184">In the Sign On URL textbox, type the URL used by your users to sign-on to your Pluralsight application using the following pattern: `https://<instance name>.pluralsight.com/sso/<comapny name>`</span><span class="sxs-lookup"><span data-stu-id="28568-184">In the Sign On URL textbox, type the URL used by your users to sign-on to your Pluralsight application using the following pattern: `https://<instance name>.pluralsight.com/sso/<comapny name>`</span></span>
  2. <span data-ttu-id="28568-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-185">Click **Next**.</span></span>
9. <span data-ttu-id="28568-186">On the **Configure single sign-on at Pluralsight** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-186">On the **Configure single sign-on at Pluralsight** page, perform the following steps:</span></span>

  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_05.png)   
  1. <span data-ttu-id="28568-188">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="28568-188">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="28568-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-189">Click **Next**.</span></span>
10. <span data-ttu-id="28568-190">To get SSO configured for your application, contact Pluralsight [Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="28568-190">To get SSO configured for your application, contact Pluralsight [Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>
11. <span data-ttu-id="28568-191">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-191">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
12. <span data-ttu-id="28568-193">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="28568-193">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="28568-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="28568-195">Create an Azure AD test user</span></span>
<span data-ttu-id="28568-196">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28568-196">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

* <span data-ttu-id="28568-197">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="28568-197">In the Users list, select **Britta Simon**.</span></span>

  ![Create Azure AD User][20]

<span data-ttu-id="28568-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="28568-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28568-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28568-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="28568-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="28568-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="28568-203">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="28568-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="28568-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="28568-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="28568-207">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="28568-209">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="28568-209">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="28568-210">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28568-210">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="28568-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-211">Click **Next**.</span></span>
6. <span data-ttu-id="28568-212">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-212">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="28568-214">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="28568-214">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="28568-215">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="28568-215">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="28568-216">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="28568-216">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="28568-217">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="28568-217">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="28568-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="28568-218">Click **Next**.</span></span>
7. <span data-ttu-id="28568-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="28568-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="28568-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="28568-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="28568-223">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="28568-223">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="28568-224">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="28568-224">Click **Complete**.</span></span>   

### <a name="create-a-pluralsight-test-user"></a><span data-ttu-id="28568-225">Create a Pluralsight test user</span><span class="sxs-lookup"><span data-stu-id="28568-225">Create a Pluralsight test user</span></span>
<span data-ttu-id="28568-226">The objective of this section is to create a user called Britta Simon in Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="28568-226">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="28568-227">Please work with Pluralsight support team to add the users in the Pluralsight account.</span><span class="sxs-lookup"><span data-stu-id="28568-227">Please work with Pluralsight support team to add the users in the Pluralsight account.</span></span> 

>[!NOTE]
><span data-ttu-id="28568-228">If you need to create an user manually, you need to contact the Pluralsight support team.</span><span class="sxs-lookup"><span data-stu-id="28568-228">If you need to create an user manually, you need to contact the Pluralsight support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="28568-229">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="28568-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="28568-230">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="28568-230">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Pluralsight.</span></span>

![Assign User][200] 

<span data-ttu-id="28568-232">**To assign Britta Simon to Pluralsight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="28568-232">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="28568-233">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="28568-233">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="28568-235">In the applications list, select **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="28568-235">In the applications list, select **Pluralsight**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_50.png) 
3. <span data-ttu-id="28568-237">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="28568-237">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="28568-239">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="28568-239">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="28568-240">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="28568-240">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="28568-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="28568-242">Test single sign-on</span></span>
<span data-ttu-id="28568-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="28568-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="28568-244">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="28568-244">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28568-245">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="28568-245">Additional Resources</span></span>
* [<span data-ttu-id="28568-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28568-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28568-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28568-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pluralsight-tutorial/tutorial_general_205.png































