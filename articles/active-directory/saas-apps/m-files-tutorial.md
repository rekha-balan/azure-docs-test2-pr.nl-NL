---
title: 'Tutorial: Azure Active Directory integration with M-Files | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and M-Files.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 41b53cb785679dec47ead99188e5cefbb132d87a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857967"
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="ae99b-103">Tutorial: Azure Active Directory integration with M-Files</span><span class="sxs-lookup"><span data-stu-id="ae99b-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="ae99b-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae99b-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae99b-105">Integrating M-Files with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ae99b-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae99b-106">You can control in Azure AD who has access to M-Files</span><span class="sxs-lookup"><span data-stu-id="ae99b-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="ae99b-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ae99b-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae99b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae99b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae99b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ae99b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae99b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae99b-110">Prerequisites</span></span>

<span data-ttu-id="ae99b-111">To configure Azure AD integration with M-Files, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ae99b-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="ae99b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ae99b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae99b-113">A M-Files single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ae99b-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae99b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ae99b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae99b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ae99b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae99b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ae99b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae99b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae99b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae99b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ae99b-118">Scenario description</span></span>
<span data-ttu-id="ae99b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ae99b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae99b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae99b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae99b-121">Adding M-Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae99b-121">Adding M-Files from the gallery</span></span>
1. <span data-ttu-id="ae99b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae99b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="ae99b-123">Adding M-Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae99b-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="ae99b-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ae99b-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae99b-125">**To add M-Files from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae99b-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae99b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae99b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ae99b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae99b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ae99b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ae99b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ae99b-133">In the search box, type **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-133">In the search box, type **M-Files**.</span></span>

    ![Creating an Azure AD test user](./media/m-files-tutorial/tutorial_m-files_search.png)

1. <span data-ttu-id="ae99b-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae99b-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae99b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae99b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae99b-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae99b-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae99b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae99b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="ae99b-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ae99b-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="ae99b-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ae99b-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae99b-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae99b-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae99b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ae99b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ae99b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae99b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ae99b-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ae99b-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ae99b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae99b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ae99b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ae99b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae99b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae99b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae99b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span><span class="sxs-lookup"><span data-stu-id="ae99b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="ae99b-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae99b-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="ae99b-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ae99b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae99b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m-files_samlbase.png)

1. <span data-ttu-id="ae99b-155">On the **M-Files Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae99b-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="ae99b-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae99b-157">a.</span></span> <span data-ttu-id="ae99b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="ae99b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="ae99b-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae99b-159">b.</span></span> <span data-ttu-id="ae99b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="ae99b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae99b-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ae99b-161">These values are not real.</span></span> <span data-ttu-id="ae99b-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ae99b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ae99b-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ae99b-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
1. <span data-ttu-id="ae99b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ae99b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m-files_certificate.png) 

1. <span data-ttu-id="ae99b-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ae99b-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ae99b-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span><span class="sxs-lookup"><span data-stu-id="ae99b-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ae99b-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span><span class="sxs-lookup"><span data-stu-id="ae99b-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="ae99b-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span><span class="sxs-lookup"><span data-stu-id="ae99b-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

1. <span data-ttu-id="ae99b-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae99b-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="ae99b-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span><span class="sxs-lookup"><span data-stu-id="ae99b-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

1. <span data-ttu-id="ae99b-173">Open the **M-Files Desktop Settings** window.</span><span class="sxs-lookup"><span data-stu-id="ae99b-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="ae99b-174">Then, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-174">Then, click **Add**.</span></span>
   
    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m_files_10.png)

1. <span data-ttu-id="ae99b-176">On the **Document Vault Connection Properties** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae99b-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="ae99b-178">Under the Server section type, the values as follows:</span><span class="sxs-lookup"><span data-stu-id="ae99b-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="ae99b-179">a.</span><span class="sxs-lookup"><span data-stu-id="ae99b-179">a.</span></span> <span data-ttu-id="ae99b-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="ae99b-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="ae99b-181">b.</span><span class="sxs-lookup"><span data-stu-id="ae99b-181">b.</span></span> <span data-ttu-id="ae99b-182">For **Port Number**, type **4466**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="ae99b-183">c.</span><span class="sxs-lookup"><span data-stu-id="ae99b-183">c.</span></span> <span data-ttu-id="ae99b-184">For **Protocol**, select **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="ae99b-185">d.</span><span class="sxs-lookup"><span data-stu-id="ae99b-185">d.</span></span> <span data-ttu-id="ae99b-186">In the **Authentication** field, select **Specific Windows user**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="ae99b-187">Then, you are prompted with a signing page.</span><span class="sxs-lookup"><span data-stu-id="ae99b-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="ae99b-188">Insert your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="ae99b-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="ae99b-189">e.</span><span class="sxs-lookup"><span data-stu-id="ae99b-189">e.</span></span> <span data-ttu-id="ae99b-190">For the **Vault on Server**,  select the corresponding vault on server.</span><span class="sxs-lookup"><span data-stu-id="ae99b-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="ae99b-191">f.</span><span class="sxs-lookup"><span data-stu-id="ae99b-191">f.</span></span> <span data-ttu-id="ae99b-192">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="ae99b-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="ae99b-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae99b-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="ae99b-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae99b-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae99b-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae99b-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae99b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae99b-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae99b-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ae99b-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae99b-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae99b-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae99b-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/m-files-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ae99b-202">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/m-files-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ae99b-204">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ae99b-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/m-files-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="ae99b-206">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae99b-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae99b-208">a.</span><span class="sxs-lookup"><span data-stu-id="ae99b-208">a.</span></span> <span data-ttu-id="ae99b-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae99b-210">b.</span><span class="sxs-lookup"><span data-stu-id="ae99b-210">b.</span></span> <span data-ttu-id="ae99b-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae99b-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae99b-212">c.</span><span class="sxs-lookup"><span data-stu-id="ae99b-212">c.</span></span> <span data-ttu-id="ae99b-213">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae99b-214">d.</span><span class="sxs-lookup"><span data-stu-id="ae99b-214">d.</span></span> <span data-ttu-id="ae99b-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="ae99b-216">Creating a M-Files test user</span><span class="sxs-lookup"><span data-stu-id="ae99b-216">Creating a M-Files test user</span></span>

<span data-ttu-id="ae99b-217">The objective of this section is to create a user called Britta Simon in M-Files.</span><span class="sxs-lookup"><span data-stu-id="ae99b-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="ae99b-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span><span class="sxs-lookup"><span data-stu-id="ae99b-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae99b-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae99b-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae99b-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span><span class="sxs-lookup"><span data-stu-id="ae99b-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Assign User][200] 

<span data-ttu-id="ae99b-222">**To assign Britta Simon to M-Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae99b-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="ae99b-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ae99b-225">In the applications list, select **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-225">In the applications list, select **M-Files**.</span></span>

    ![Configure Single Sign-On](./media/m-files-tutorial/tutorial_m-files_app.png) 

1. <span data-ttu-id="ae99b-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ae99b-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="ae99b-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ae99b-229">Click **Add** button.</span></span> <span data-ttu-id="ae99b-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae99b-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ae99b-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ae99b-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ae99b-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae99b-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ae99b-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae99b-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae99b-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae99b-235">Testing single sign-on</span></span>

<span data-ttu-id="ae99b-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae99b-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ae99b-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span><span class="sxs-lookup"><span data-stu-id="ae99b-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae99b-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ae99b-238">Additional resources</span></span>

* [<span data-ttu-id="ae99b-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae99b-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ae99b-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae99b-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/m-files-tutorial/tutorial_general_01.png
[2]: ./media/m-files-tutorial/tutorial_general_02.png
[3]: ./media/m-files-tutorial/tutorial_general_03.png
[4]: ./media/m-files-tutorial/tutorial_general_04.png

[100]: ./media/m-files-tutorial/tutorial_general_100.png

[200]: ./media/m-files-tutorial/tutorial_general_200.png
[201]: ./media/m-files-tutorial/tutorial_general_201.png
[202]: ./media/m-files-tutorial/tutorial_general_202.png
[203]: ./media/m-files-tutorial/tutorial_general_203.png

