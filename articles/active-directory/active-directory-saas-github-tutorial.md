---
title: 'Tutorial: Azure Active Directory integration with GitHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: jeedes
ms.openlocfilehash: 55ee12df4e8553482ded563637590351152e91ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551239"
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="330d6-103">Tutorial: Azure Active Directory integration with GitHub</span><span class="sxs-lookup"><span data-stu-id="330d6-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="330d6-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="330d6-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="330d6-105">Integrating GitHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="330d6-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="330d6-106">You can control in Azure AD who has access to GitHub</span><span class="sxs-lookup"><span data-stu-id="330d6-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="330d6-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="330d6-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="330d6-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="330d6-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="330d6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="330d6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="330d6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="330d6-110">Prerequisites</span></span>

<span data-ttu-id="330d6-111">To configure Azure AD integration with GitHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="330d6-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="330d6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="330d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="330d6-113">A GitHub single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="330d6-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="330d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="330d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="330d6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="330d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="330d6-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="330d6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="330d6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="330d6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="330d6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="330d6-118">Scenario description</span></span>
<span data-ttu-id="330d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="330d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="330d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="330d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="330d6-121">Adding GitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="330d6-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="330d6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="330d6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="330d6-123">Adding GitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="330d6-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="330d6-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="330d6-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="330d6-125">**To add GitHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="330d6-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="330d6-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="330d6-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="330d6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="330d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="330d6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="330d6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="330d6-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="330d6-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="330d6-133">In the search box, type **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="330d6-133">In the search box, type **GitHub.com**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="330d6-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="330d6-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="330d6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="330d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="330d6-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="330d6-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="330d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="330d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="330d6-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="330d6-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="330d6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span><span class="sxs-lookup"><span data-stu-id="330d6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="330d6-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="330d6-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="330d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="330d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="330d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="330d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="330d6-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="330d6-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="330d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="330d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="330d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="330d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="330d6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="330d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="330d6-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span><span class="sxs-lookup"><span data-stu-id="330d6-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="330d6-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="330d6-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="330d6-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="330d6-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="330d6-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="330d6-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="330d6-155">On the **GitHub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="330d6-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="330d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="330d6-157">a.</span></span> <span data-ttu-id="330d6-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="330d6-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="330d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="330d6-159">b.</span></span> <span data-ttu-id="330d6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="330d6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="330d6-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="330d6-161">Please note that these are not the real values.</span></span> <span data-ttu-id="330d6-162">You have to update these values with the actual Sing-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="330d6-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="330d6-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="330d6-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="330d6-164">Go to GitHub Admin section to retrieve these values.</span><span class="sxs-lookup"><span data-stu-id="330d6-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="330d6-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span><span class="sxs-lookup"><span data-stu-id="330d6-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="330d6-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="330d6-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="330d6-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="330d6-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="330d6-170">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="330d6-170">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="330d6-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="330d6-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="330d6-174">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="330d6-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="330d6-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="330d6-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="330d6-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="330d6-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="330d6-181">In a different web browser window, log into your GitHub organization site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="330d6-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="330d6-182">Navigate to **Settings** and click **Security**</span><span class="sxs-lookup"><span data-stu-id="330d6-182">Navigate to **Settings** and click **Security**</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="330d6-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span><span class="sxs-lookup"><span data-stu-id="330d6-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="330d6-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span><span class="sxs-lookup"><span data-stu-id="330d6-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="330d6-187">Configure the following fields:</span><span class="sxs-lookup"><span data-stu-id="330d6-187">Configure the following fields:</span></span>

    <span data-ttu-id="330d6-188">a.</span><span class="sxs-lookup"><span data-stu-id="330d6-188">a.</span></span> <span data-ttu-id="330d6-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span><span class="sxs-lookup"><span data-stu-id="330d6-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="330d6-190">b.</span><span class="sxs-lookup"><span data-stu-id="330d6-190">b.</span></span> <span data-ttu-id="330d6-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span><span class="sxs-lookup"><span data-stu-id="330d6-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="330d6-192">c.</span><span class="sxs-lookup"><span data-stu-id="330d6-192">c.</span></span> <span data-ttu-id="330d6-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="330d6-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="330d6-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span><span class="sxs-lookup"><span data-stu-id="330d6-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="330d6-197">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="330d6-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="330d6-198">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="330d6-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="330d6-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="330d6-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="330d6-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="330d6-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="330d6-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="330d6-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="330d6-204">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="330d6-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="330d6-206">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="330d6-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="330d6-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="330d6-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="330d6-210">a.</span><span class="sxs-lookup"><span data-stu-id="330d6-210">a.</span></span> <span data-ttu-id="330d6-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="330d6-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="330d6-212">b.</span><span class="sxs-lookup"><span data-stu-id="330d6-212">b.</span></span> <span data-ttu-id="330d6-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="330d6-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="330d6-214">c.</span><span class="sxs-lookup"><span data-stu-id="330d6-214">c.</span></span> <span data-ttu-id="330d6-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="330d6-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="330d6-216">d.</span><span class="sxs-lookup"><span data-stu-id="330d6-216">d.</span></span> <span data-ttu-id="330d6-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="330d6-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="330d6-218">Creating a GitHub test user</span><span class="sxs-lookup"><span data-stu-id="330d6-218">Creating a GitHub test user</span></span>

<span data-ttu-id="330d6-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span><span class="sxs-lookup"><span data-stu-id="330d6-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="330d6-220">In the case of GitHub, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="330d6-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="330d6-221">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="330d6-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="330d6-222">Log in to your GitHub company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="330d6-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="330d6-223">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="330d6-223">Click **People**.</span></span>

    <span data-ttu-id="330d6-224">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span><span class="sxs-lookup"><span data-stu-id="330d6-224">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="330d6-225">Click **Invite member**.</span><span class="sxs-lookup"><span data-stu-id="330d6-225">Click **Invite member**.</span></span>

    <span data-ttu-id="330d6-226">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="330d6-226">![Invite Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="330d6-227">On the **Invite member** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="330d6-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="330d6-228">a.</span><span class="sxs-lookup"><span data-stu-id="330d6-228">a.</span></span> <span data-ttu-id="330d6-229">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="330d6-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="330d6-230">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="330d6-230">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="330d6-231">b.</span><span class="sxs-lookup"><span data-stu-id="330d6-231">b.</span></span> <span data-ttu-id="330d6-232">Click **Send Invitation**.</span><span class="sxs-lookup"><span data-stu-id="330d6-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="330d6-233">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="330d6-233">![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="330d6-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="330d6-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="330d6-235">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="330d6-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="330d6-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span><span class="sxs-lookup"><span data-stu-id="330d6-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Assign User][200] 

<span data-ttu-id="330d6-238">**To assign Britta Simon to GitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="330d6-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="330d6-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="330d6-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="330d6-241">In the applications list, select **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="330d6-241">In the applications list, select **GitHub.com**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="330d6-243">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="330d6-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="330d6-245">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="330d6-245">Click **Add** button.</span></span> <span data-ttu-id="330d6-246">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="330d6-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="330d6-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="330d6-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="330d6-249">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="330d6-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="330d6-250">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="330d6-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="330d6-251">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="330d6-251">Testing single sign-on</span></span>

<span data-ttu-id="330d6-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="330d6-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="330d6-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span><span class="sxs-lookup"><span data-stu-id="330d6-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="330d6-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span><span class="sxs-lookup"><span data-stu-id="330d6-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="330d6-255">Additional resources</span><span class="sxs-lookup"><span data-stu-id="330d6-255">Additional resources</span></span>

* [<span data-ttu-id="330d6-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="330d6-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="330d6-257">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="330d6-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-github-tutorial/tutorial_general_203.png


































