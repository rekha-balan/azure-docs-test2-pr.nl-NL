---
title: 'Tutorial: Azure Active Directory integration with M-Files | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and M-Files.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: 9860fbcef5e89c5f1a7ae0cd71d62370270d1243
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669959"
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="f28b5-103">Tutorial: Azure Active Directory integration with M-Files</span><span class="sxs-lookup"><span data-stu-id="f28b5-103">Tutorial: Azure Active Directory integration with M-Files</span></span>
<span data-ttu-id="f28b5-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f28b5-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f28b5-105">Integrating M-Files with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f28b5-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="f28b5-106">You can control in Azure AD who has access to M-Files</span><span class="sxs-lookup"><span data-stu-id="f28b5-106">You can control in Azure AD who has access to M-Files</span></span>
* <span data-ttu-id="f28b5-107">You can enable your users to automatically get signed-on to M-Files single sign-on (SSO)) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f28b5-107">You can enable your users to automatically get signed-on to M-Files single sign-on (SSO)) with their Azure AD accounts</span></span>
* <span data-ttu-id="f28b5-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="f28b5-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f28b5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f28b5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f28b5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f28b5-110">Prerequisites</span></span>
<span data-ttu-id="f28b5-111">To configure Azure AD integration with M-Files, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f28b5-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

* <span data-ttu-id="f28b5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f28b5-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f28b5-113">A **M-Files** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f28b5-113">A **M-Files** SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="f28b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f28b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="f28b5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f28b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f28b5-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f28b5-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f28b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f28b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f28b5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f28b5-118">Scenario description</span></span>
<span data-ttu-id="f28b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f28b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f28b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f28b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f28b5-121">Adding M-Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="f28b5-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="f28b5-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="f28b5-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="f28b5-123">Adding M-Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="f28b5-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="f28b5-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f28b5-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f28b5-125">**To add M-Files from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28b5-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f28b5-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="f28b5-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f28b5-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f28b5-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f28b5-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="f28b5-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f28b5-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="f28b5-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="f28b5-135">In the search box, type **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-135">In the search box, type **M-Files**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_01.png)
7. <span data-ttu-id="f28b5-137">In the results pane, select **M-Files**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f28b5-137">In the results pane, select **M-Files**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="f28b5-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="f28b5-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="f28b5-140">In this section, you configure and test Azure AD SSO with M-Files based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f28b5-140">In this section, you configure and test Azure AD SSO with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f28b5-141">For SSO to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f28b5-141">For SSO to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="f28b5-142">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f28b5-142">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="f28b5-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in M-Files.</span><span class="sxs-lookup"><span data-stu-id="f28b5-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in M-Files.</span></span> <span data-ttu-id="f28b5-144">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f28b5-144">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f28b5-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f28b5-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f28b5-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f28b5-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f28b5-147">**[Creating a M-Files test user](#creating-a-m-file-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="f28b5-147">**[Creating a M-Files test user](#creating-a-m-file-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f28b5-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f28b5-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f28b5-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f28b5-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="f28b5-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="f28b5-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="f28b5-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your M-Files application.</span><span class="sxs-lookup"><span data-stu-id="f28b5-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your M-Files application.</span></span>

<span data-ttu-id="f28b5-152">**To configure Azure AD SSO with M-Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28b5-152">**To configure Azure AD SSO with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="f28b5-153">In the classic portal, on the **M-Files** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="f28b5-153">In the classic portal, on the **M-Files** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
2. <span data-ttu-id="f28b5-155">On the **How would you like users to sign on to M-Files** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-155">On the **How would you like users to sign on to M-Files** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_06.png)
3. <span data-ttu-id="f28b5-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28b5-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_07.png)
  1. <span data-ttu-id="f28b5-159">In the Sign On URL textbox, type a URL using the following pattern: `https://<tenant-name>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="f28b5-159">In the Sign On URL textbox, type a URL using the following pattern: `https://<tenant-name>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>
  2. <span data-ttu-id="f28b5-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-160">Click **Next**.</span></span>
4. <span data-ttu-id="f28b5-161">On the **Configure single sign-on at M-Files** page, Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f28b5-161">On the **Configure single sign-on at M-Files** page, Click **Download metadata**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_09.png)
5. <span data-ttu-id="f28b5-163">To get SSO configured for your application, contact M-files support team via <mailto:support@m-files.com> and provide them with the the downloaded Metadata.</span><span class="sxs-lookup"><span data-stu-id="f28b5-163">To get SSO configured for your application, contact M-files support team via <mailto:support@m-files.com> and provide them with the the downloaded Metadata.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f28b5-164">Follow the next steps if you want to configure SSO for you M-File desktop application.</span><span class="sxs-lookup"><span data-stu-id="f28b5-164">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="f28b5-165">No extra steps are required if you only want to configure SSO for M-Files web version.</span><span class="sxs-lookup"><span data-stu-id="f28b5-165">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  
   > 
6. <span data-ttu-id="f28b5-166">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f28b5-166">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="f28b5-167">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span><span class="sxs-lookup"><span data-stu-id="f28b5-167">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>
7. <span data-ttu-id="f28b5-168">Open the **M-Files Desktop Settings** window.</span><span class="sxs-lookup"><span data-stu-id="f28b5-168">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="f28b5-169">Then, click on **Add**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-169">Then, click on **Add**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)
8. <span data-ttu-id="f28b5-171">On the **Document Vault Connection Properties** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28b5-171">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
  <span data-ttu-id="f28b5-172">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)</span><span class="sxs-lookup"><span data-stu-id="f28b5-172">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)</span></span>  
    <span data-ttu-id="f28b5-173">Under the **Server** section type the values as follow:</span><span class="sxs-lookup"><span data-stu-id="f28b5-173">Under the **Server** section type the values as follow:</span></span>  
 1. <span data-ttu-id="f28b5-174">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="f28b5-174">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span>  
 2. <span data-ttu-id="f28b5-175">For **Port Number**, type **4466**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-175">For **Port Number**, type **4466**.</span></span> 
 3. <span data-ttu-id="f28b5-176">For **Protocol**, select **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-176">For **Protocol**, select **HTTPS**.</span></span> 
 4. <span data-ttu-id="f28b5-177">In the **Authentication** field, select **Specific Windows user**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-177">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="f28b5-178">Then, you will be prompted with a signing page.</span><span class="sxs-lookup"><span data-stu-id="f28b5-178">Then, you will be prompted with a signing page.</span></span> <span data-ttu-id="f28b5-179">Please insert your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="f28b5-179">Please insert your Azure AD credentials.</span></span> 
 5. <span data-ttu-id="f28b5-180">For the **Vault on Server**,  select the corresponding vault on server.</span><span class="sxs-lookup"><span data-stu-id="f28b5-180">For the **Vault on Server**,  select the corresponding vault on server.</span></span> 
 6. <span data-ttu-id="f28b5-181">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-181">Click **OK**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f28b5-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f28b5-182">Create an Azure AD test user</span></span>
<span data-ttu-id="f28b5-183">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f28b5-183">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="f28b5-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28b5-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f28b5-186">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-186">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="f28b5-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f28b5-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f28b5-189">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-189">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="f28b5-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="f28b5-193">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28b5-193">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="f28b5-195">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="f28b5-195">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="f28b5-196">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-196">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="f28b5-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-197">Click **Next**.</span></span>
6. <span data-ttu-id="f28b5-198">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28b5-198">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="f28b5-200">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-200">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="f28b5-201">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-201">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="f28b5-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-202">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="f28b5-203">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-203">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="f28b5-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-204">Click **Next**.</span></span>
7. <span data-ttu-id="f28b5-205">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-205">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="f28b5-207">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28b5-207">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="f28b5-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-209">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="f28b5-210">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-210">Click **Complete**.</span></span>   

### <a name="create-a-m-files-test-user"></a><span data-ttu-id="f28b5-211">Create a M-Files test user</span><span class="sxs-lookup"><span data-stu-id="f28b5-211">Create a M-Files test user</span></span>
<span data-ttu-id="f28b5-212">In this section, you create a user called Britta Simon in M-Files.</span><span class="sxs-lookup"><span data-stu-id="f28b5-212">In this section, you create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="f28b5-213">If you don't know how to create a user in M-Files, please contact M-Files support at <mailto:support@m-files.com>.</span><span class="sxs-lookup"><span data-stu-id="f28b5-213">If you don't know how to create a user in M-Files, please contact M-Files support at <mailto:support@m-files.com>.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f28b5-214">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f28b5-214">Assign the Azure AD test user</span></span>
<span data-ttu-id="f28b5-215">In this section, you enable Britta Simon to use Azure SSO by granting her access to M-Files.</span><span class="sxs-lookup"><span data-stu-id="f28b5-215">In this section, you enable Britta Simon to use Azure SSO by granting her access to M-Files.</span></span>

![Assign User][200]

<span data-ttu-id="f28b5-217">**To assign Britta Simon to M-Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28b5-217">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="f28b5-218">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f28b5-218">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="f28b5-220">In the applications list, select **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-220">In the applications list, select **M-Files**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_m_files_12.png)
3. <span data-ttu-id="f28b5-222">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-222">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="f28b5-224">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-224">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="f28b5-225">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="f28b5-225">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f28b5-227">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f28b5-227">Test single sign-on</span></span>
<span data-ttu-id="f28b5-228">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f28b5-228">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f28b5-229">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span><span class="sxs-lookup"><span data-stu-id="f28b5-229">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f28b5-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f28b5-230">Additional resources</span></span>
* [<span data-ttu-id="f28b5-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f28b5-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f28b5-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f28b5-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-m-files-tutorial/tutorial_general_205.png





























