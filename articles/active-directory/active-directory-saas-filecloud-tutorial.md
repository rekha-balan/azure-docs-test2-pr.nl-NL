---
title: 'Tutorial: Azure Active Directory integration with FileCloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FileCloud.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: be43afb6e478729d3979cacecee7df50b9219a5b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661191"
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="d1f64-103">Tutorial: Azure Active Directory integration with FileCloud</span><span class="sxs-lookup"><span data-stu-id="d1f64-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>
<span data-ttu-id="d1f64-104">The objective of this tutorial is to show you how to integrate FileCloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1f64-104">The objective of this tutorial is to show you how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1f64-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d1f64-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d1f64-106">You can control in Azure AD who has access to FileCloud</span><span class="sxs-lookup"><span data-stu-id="d1f64-106">You can control in Azure AD who has access to FileCloud</span></span>
* <span data-ttu-id="d1f64-107">You can enable your users to automatically get signed-on to FileCloud single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d1f64-107">You can enable your users to automatically get signed-on to FileCloud single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d1f64-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d1f64-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d1f64-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1f64-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1f64-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1f64-110">Prerequisites</span></span>
<span data-ttu-id="d1f64-111">To configure Azure AD integration with FileCloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d1f64-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

* <span data-ttu-id="d1f64-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d1f64-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d1f64-113">A FileCloud SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d1f64-113">A FileCloud SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d1f64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d1f64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d1f64-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d1f64-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d1f64-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d1f64-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d1f64-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1f64-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1f64-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d1f64-118">Scenario description</span></span>
<span data-ttu-id="d1f64-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d1f64-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="d1f64-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d1f64-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1f64-121">Adding FileCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="d1f64-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="d1f64-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d1f64-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-filecloud-from-the-gallery"></a><span data-ttu-id="d1f64-123">Add FileCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="d1f64-123">Add FileCloud from the gallery</span></span>
<span data-ttu-id="d1f64-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d1f64-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1f64-125">**To add FileCloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d1f64-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1f64-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="d1f64-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d1f64-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="d1f64-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d1f64-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="d1f64-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d1f64-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="d1f64-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="d1f64-135">In the search box, type **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-135">In the search box, type **FileCloud**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_01.png)

7. <span data-ttu-id="d1f64-137">In the results panel, select **FileCloud**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d1f64-137">In the results panel, select **FileCloud**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d1f64-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d1f64-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d1f64-140">The objective of this section is to show you how to configure and test Azure AD SSO with FileCloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d1f64-140">The objective of this section is to show you how to configure and test Azure AD SSO with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1f64-141">For SSO to work, Azure AD needs to know what the counterpart user in FileCloud to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="d1f64-141">For SSO to work, Azure AD needs to know what the counterpart user in FileCloud to an user in Azure AD is.</span></span> <span data-ttu-id="d1f64-142">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d1f64-142">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="d1f64-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FileCloud.</span><span class="sxs-lookup"><span data-stu-id="d1f64-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FileCloud.</span></span>

<span data-ttu-id="d1f64-144">To configure and test Azure AD SSO with FileCloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d1f64-144">To configure and test Azure AD SSO with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1f64-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d1f64-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1f64-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1f64-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1f64-147">**[Creating a FileCloud test user](#creating-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d1f64-147">**[Creating a FileCloud test user](#creating-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d1f64-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d1f64-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1f64-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d1f64-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d1f64-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d1f64-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="d1f64-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your FileCloud application.</span><span class="sxs-lookup"><span data-stu-id="d1f64-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your FileCloud application.</span></span>

<span data-ttu-id="d1f64-152">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d1f64-152">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d1f64-153">In the classic portal, on the **FileCloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d1f64-153">In the classic portal, on the **FileCloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="d1f64-155">On the **How would you like users to sign on to FileCloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-155">On the **How would you like users to sign on to FileCloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_03.png)

3. <span data-ttu-id="d1f64-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="d1f64-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_04.png)
  1. <span data-ttu-id="d1f64-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`.</span><span class="sxs-lookup"><span data-stu-id="d1f64-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`.</span></span>
  2. <span data-ttu-id="d1f64-160">In the **Identifier** textbox, type: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`.</span><span class="sxs-lookup"><span data-stu-id="d1f64-160">In the **Identifier** textbox, type: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`.</span></span>
  3. <span data-ttu-id="d1f64-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-161">Click **Next**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d1f64-162">Please note that you have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="d1f64-162">Please note that you have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="d1f64-163">To get these values, contact FileCloud support team via <mailto:support@codelathe.com>.</span><span class="sxs-lookup"><span data-stu-id="d1f64-163">To get these values, contact FileCloud support team via <mailto:support@codelathe.com>.</span></span>
    >  

4. <span data-ttu-id="d1f64-164">On the **Configure single sign-on at FileCloud** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="d1f64-164">On the **Configure single sign-on at FileCloud** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_05.png)
 1. <span data-ttu-id="d1f64-166">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d1f64-166">Click **Download metadata**, and then save the file on your computer.</span></span>
 2. <span data-ttu-id="d1f64-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-167">Click **Next**.</span></span>

5. <span data-ttu-id="d1f64-168">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d1f64-168">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

6. <span data-ttu-id="d1f64-169">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-169">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

7. <span data-ttu-id="d1f64-171">Click **SSO** tab on Settings section.</span><span class="sxs-lookup"><span data-stu-id="d1f64-171">Click **SSO** tab on Settings section.</span></span> 
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

8. <span data-ttu-id="d1f64-173">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span><span class="sxs-lookup"><span data-stu-id="d1f64-173">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

9. <span data-ttu-id="d1f64-175">In the **IdP End Point URL** textbox put the value of **Entity ID** from Azure AD application configuration wizard on **SAML Settings** panel.</span><span class="sxs-lookup"><span data-stu-id="d1f64-175">In the **IdP End Point URL** textbox put the value of **Entity ID** from Azure AD application configuration wizard on **SAML Settings** panel.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

10. <span data-ttu-id="d1f64-177">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span><span class="sxs-lookup"><span data-stu-id="d1f64-177">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

11. <span data-ttu-id="d1f64-179">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d1f64-179">Click **Save** button.</span></span>

12. <span data-ttu-id="d1f64-180">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-180">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

13. <span data-ttu-id="d1f64-182">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-182">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d1f64-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d1f64-184">Create an Azure AD test user</span></span>
<span data-ttu-id="d1f64-185">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1f64-185">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d1f64-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d1f64-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1f64-188">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-188">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_09.png)

2. <span data-ttu-id="d1f64-190">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d1f64-190">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="d1f64-191">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-191">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d1f64-193">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-193">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

5. <span data-ttu-id="d1f64-195">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d1f64-195">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_05.png)
 1. <span data-ttu-id="d1f64-197">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d1f64-197">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="d1f64-198">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-198">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="d1f64-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-199">Click **Next**.</span></span>

6. <span data-ttu-id="d1f64-200">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d1f64-200">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="d1f64-202">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-202">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="d1f64-203">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-203">In the **Last Name** textbox, type **Simon**.</span></span> 
 3. <span data-ttu-id="d1f64-204">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-204">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="d1f64-205">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-205">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="d1f64-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-206">Click **Next**.</span></span>

7. <span data-ttu-id="d1f64-207">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-207">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_07.png)

8. <span data-ttu-id="d1f64-209">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d1f64-209">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="d1f64-211">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-211">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="d1f64-212">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-212">Click **Complete**.</span></span>   

### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="d1f64-213">Create a FileCloud test user</span><span class="sxs-lookup"><span data-stu-id="d1f64-213">Create a FileCloud test user</span></span>
<span data-ttu-id="d1f64-214">The objective of this section is to create a user called Britta Simon in FileCloud.</span><span class="sxs-lookup"><span data-stu-id="d1f64-214">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="d1f64-215">FileCloud supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="d1f64-215">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d1f64-216">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d1f64-216">There is no action item for you in this section.</span></span> <span data-ttu-id="d1f64-217">A new user will be created during an attempt to access FileCloud if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="d1f64-217">A new user will be created during an attempt to access FileCloud if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="d1f64-218">If you need to create an user manually, you need to contact the FileCloud support team.</span><span class="sxs-lookup"><span data-stu-id="d1f64-218">If you need to create an user manually, you need to contact the FileCloud support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d1f64-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d1f64-219">Assign the Azure AD test user</span></span>
<span data-ttu-id="d1f64-220">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to FileCloud.</span><span class="sxs-lookup"><span data-stu-id="d1f64-220">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to FileCloud.</span></span>

![Assign User][200]

<span data-ttu-id="d1f64-222">**To assign Britta Simon to FileCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d1f64-222">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d1f64-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d1f64-223">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]

2. <span data-ttu-id="d1f64-225">In the applications list, select **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-225">In the applications list, select **FileCloud**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_50.png)

3. <span data-ttu-id="d1f64-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-227">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="d1f64-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-229">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="d1f64-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d1f64-230">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d1f64-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d1f64-232">Test single sign-on</span></span>
<span data-ttu-id="d1f64-233">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d1f64-233">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d1f64-234">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span><span class="sxs-lookup"><span data-stu-id="d1f64-234">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1f64-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d1f64-235">Additional resources</span></span>
* [<span data-ttu-id="d1f64-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1f64-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1f64-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1f64-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-filecloud-tutorial/tutorial_general_205.png






























