---
title: 'Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Veritas Enterprise Vault.cloud SSO.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 66cd4e9198202d237793d758fb1e7d9c376d8129
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555460"
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="edfd6-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="edfd6-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="edfd6-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edfd6-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edfd6-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="edfd6-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="edfd6-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="edfd6-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="edfd6-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="edfd6-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edfd6-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="edfd6-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="edfd6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edfd6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edfd6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edfd6-110">Prerequisites</span></span>

<span data-ttu-id="edfd6-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="edfd6-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span></span>

- <span data-ttu-id="edfd6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="edfd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edfd6-113">A Veritas Enterprise Vault.cloud SSO single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="edfd6-113">A Veritas Enterprise Vault.cloud SSO single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="edfd6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="edfd6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="edfd6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="edfd6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edfd6-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="edfd6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="edfd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edfd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="edfd6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="edfd6-118">Scenario description</span></span>
<span data-ttu-id="edfd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="edfd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="edfd6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="edfd6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edfd6-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="edfd6-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
2. <span data-ttu-id="edfd6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edfd6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a><span data-ttu-id="edfd6-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="edfd6-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
<span data-ttu-id="edfd6-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="edfd6-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="edfd6-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edfd6-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="edfd6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="edfd6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="edfd6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="edfd6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="edfd6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="edfd6-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="edfd6-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="edfd6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="edfd6-135">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-135">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_veritas-enterprise-vault-cloud-sso_01.png)
7. <span data-ttu-id="edfd6-137">In the results pane, select **Veritas Enterprise Vault.cloud SSO**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="edfd6-137">In the results pane, select **Veritas Enterprise Vault.cloud SSO**, and then click **Complete** to add the application.</span></span>



##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edfd6-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edfd6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edfd6-139">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="edfd6-139">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edfd6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edfd6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span></span> <span data-ttu-id="edfd6-141">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="edfd6-141">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span></span>

<span data-ttu-id="edfd6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="edfd6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Veritas Enterprise Vault.cloud SSO.</span></span>

<span data-ttu-id="edfd6-143">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="edfd6-143">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="edfd6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="edfd6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="edfd6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edfd6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edfd6-146">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-Veritas Enterprise Vault.cloud SSO-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="edfd6-146">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-Veritas Enterprise Vault.cloud SSO-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="edfd6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="edfd6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edfd6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="edfd6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edfd6-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edfd6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edfd6-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span><span class="sxs-lookup"><span data-stu-id="edfd6-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>


<span data-ttu-id="edfd6-151">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edfd6-151">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="edfd6-152">In the classic portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="edfd6-152">In the classic portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="edfd6-154">On the **How would you like users to sign on to Veritas Enterprise Vault.cloud SSO** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-154">On the **How would you like users to sign on to Veritas Enterprise Vault.cloud SSO** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_veritas-enterprise-vault-cloud-sso_03.png) 

3. <span data-ttu-id="edfd6-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="edfd6-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_veritas-enterprise-vault-cloud-sso_04.png) 

    <span data-ttu-id="edfd6-158">a.</span><span class="sxs-lookup"><span data-stu-id="edfd6-158">a.</span></span> <span data-ttu-id="edfd6-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Veritas Enterprise Vault.cloud SSO application using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="edfd6-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Veritas Enterprise Vault.cloud SSO application using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
     
4. <span data-ttu-id="edfd6-160">On the **Configure single sign-on at Veritas Enterprise Vault.cloud SSO** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="edfd6-160">On the **Configure single sign-on at Veritas Enterprise Vault.cloud SSO** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_veritas-enterprise-vault-cloud-sso_05.png)

    <span data-ttu-id="edfd6-162">a.</span><span class="sxs-lookup"><span data-stu-id="edfd6-162">a.</span></span> <span data-ttu-id="edfd6-163">Click **Download Certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="edfd6-163">Click **Download Certificate**, and then save the file on your computer.</span></span>

    <span data-ttu-id="edfd6-164">b.</span><span class="sxs-lookup"><span data-stu-id="edfd6-164">b.</span></span> <span data-ttu-id="edfd6-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-165">Click **Next**.</span></span>


5. <span data-ttu-id="edfd6-166">To get SSO configured for your application, contact Veritas Enterprise Vault.cloud SSO support team  at <a href="https://www.veritas.com/content/support/en_US/62696.html "> Support website</a>  and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="edfd6-166">To get SSO configured for your application, contact Veritas Enterprise Vault.cloud SSO support team  at <a href="https://www.veritas.com/content/support/en_US/62696.html "> Support website</a>  and provide them with the following:</span></span>

    <span data-ttu-id="edfd6-167">• The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="edfd6-167">• The downloaded **metadata**</span></span>

    <span data-ttu-id="edfd6-168">• The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="edfd6-168">• The **SAML SSO URL**</span></span>

6. <span data-ttu-id="edfd6-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="edfd6-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edfd6-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edfd6-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="edfd6-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edfd6-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Create Azure AD User][20]

<span data-ttu-id="edfd6-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edfd6-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="edfd6-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="edfd6-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="edfd6-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="edfd6-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edfd6-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="edfd6-184">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="edfd6-184">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="edfd6-185">a.</span><span class="sxs-lookup"><span data-stu-id="edfd6-185">a.</span></span> <span data-ttu-id="edfd6-186">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="edfd6-186">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="edfd6-187">b.</span><span class="sxs-lookup"><span data-stu-id="edfd6-187">b.</span></span> <span data-ttu-id="edfd6-188">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-188">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edfd6-189">c.</span><span class="sxs-lookup"><span data-stu-id="edfd6-189">c.</span></span> <span data-ttu-id="edfd6-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-190">Click **Next**.</span></span>

6.  <span data-ttu-id="edfd6-191">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="edfd6-191">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="edfd6-192">a.</span><span class="sxs-lookup"><span data-stu-id="edfd6-192">a.</span></span> <span data-ttu-id="edfd6-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-193">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="edfd6-194">b.</span><span class="sxs-lookup"><span data-stu-id="edfd6-194">b.</span></span> <span data-ttu-id="edfd6-195">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-195">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="edfd6-196">c.</span><span class="sxs-lookup"><span data-stu-id="edfd6-196">c.</span></span> <span data-ttu-id="edfd6-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="edfd6-198">d.</span><span class="sxs-lookup"><span data-stu-id="edfd6-198">d.</span></span> <span data-ttu-id="edfd6-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-199">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="edfd6-200">e.</span><span class="sxs-lookup"><span data-stu-id="edfd6-200">e.</span></span> <span data-ttu-id="edfd6-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-201">Click **Next**.</span></span>

7. <span data-ttu-id="edfd6-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-202">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="edfd6-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="edfd6-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="edfd6-206">a.</span><span class="sxs-lookup"><span data-stu-id="edfd6-206">a.</span></span> <span data-ttu-id="edfd6-207">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-207">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="edfd6-208">b.</span><span class="sxs-lookup"><span data-stu-id="edfd6-208">b.</span></span> <span data-ttu-id="edfd6-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-209">Click **Complete**.</span></span>   



### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="edfd6-210">Creating a Veritas Enterprise Vault.cloud SSO test user</span><span class="sxs-lookup"><span data-stu-id="edfd6-210">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="edfd6-211">In this section, you create a user called Britta Simon in Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="edfd6-211">In this section, you create a user called Britta Simon in Veritas Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="edfd6-212">Please work with Veritas Enterprise Vault.cloud SSO support team at <a href="https://www.veritas.com/content/support/en_US/62696.html "> Support website</a> to add the users in the Veritas Enterprise Vault.cloud SSO platform.</span><span class="sxs-lookup"><span data-stu-id="edfd6-212">Please work with Veritas Enterprise Vault.cloud SSO support team at <a href="https://www.veritas.com/content/support/en_US/62696.html "> Support website</a> to add the users in the Veritas Enterprise Vault.cloud SSO platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="edfd6-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edfd6-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="edfd6-214">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="edfd6-214">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Veritas Enterprise Vault.cloud SSO.</span></span>

![Assign User][200] 

<span data-ttu-id="edfd6-216">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edfd6-216">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="edfd6-217">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="edfd6-217">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="edfd6-219">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-219">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_veritas-enterprise-vault-cloud-sso_50.png) 

3. <span data-ttu-id="edfd6-221">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-221">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="edfd6-223">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-223">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="edfd6-224">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="edfd6-224">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="edfd6-226">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="edfd6-226">Testing Single Sign-On</span></span>

<span data-ttu-id="edfd6-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="edfd6-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="edfd6-228">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span><span class="sxs-lookup"><span data-stu-id="edfd6-228">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="edfd6-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="edfd6-229">Additional resources</span></span>

* [<span data-ttu-id="edfd6-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edfd6-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edfd6-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edfd6-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veritas-enterprise-vault-cloud-sso-tutorial/tutorial_general_205.png

























