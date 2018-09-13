---
title: 'Tutorial: Azure Active Directory integration with Pingboard | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: c0f908a13054c88640f184d96f19e13cb87dff36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555961"
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="b33d0-103">Tutorial: Azure Active Directory integration with Pingboard</span><span class="sxs-lookup"><span data-stu-id="b33d0-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="b33d0-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b33d0-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b33d0-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b33d0-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b33d0-106">You can control in Azure AD who has access to Pingboard</span><span class="sxs-lookup"><span data-stu-id="b33d0-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="b33d0-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b33d0-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b33d0-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="b33d0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="b33d0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b33d0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b33d0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b33d0-110">Prerequisites</span></span>

<span data-ttu-id="b33d0-111">To configure Azure AD integration with Pingboard, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b33d0-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="b33d0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b33d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b33d0-113">A Pingboard single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b33d0-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b33d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b33d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b33d0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b33d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b33d0-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b33d0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b33d0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b33d0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b33d0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b33d0-118">Scenario description</span></span>
<span data-ttu-id="b33d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b33d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b33d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b33d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b33d0-121">Adding Pingboard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b33d0-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="b33d0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b33d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="b33d0-123">Adding Pingboard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b33d0-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="b33d0-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b33d0-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b33d0-125">**To add Pingboard from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b33d0-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b33d0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b33d0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b33d0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b33d0-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="b33d0-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b33d0-133">In the search box, type **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-133">In the search box, type **Pingboard**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="b33d0-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b33d0-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b33d0-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b33d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b33d0-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b33d0-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b33d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b33d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="b33d0-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b33d0-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="b33d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="b33d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="b33d0-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b33d0-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b33d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b33d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b33d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b33d0-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b33d0-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b33d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b33d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b33d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b33d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b33d0-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b33d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b33d0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span><span class="sxs-lookup"><span data-stu-id="b33d0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="b33d0-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b33d0-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="b33d0-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="b33d0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="b33d0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="b33d0-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b33d0-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="b33d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="b33d0-157">a.</span></span> <span data-ttu-id="b33d0-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="b33d0-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="b33d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="b33d0-159">b.</span></span> <span data-ttu-id="b33d0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="b33d0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b33d0-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="b33d0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="b33d0-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="b33d0-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b33d0-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="b33d0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="b33d0-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b33d0-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="b33d0-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b33d0-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="b33d0-167">a.</span><span class="sxs-lookup"><span data-stu-id="b33d0-167">a.</span></span> <span data-ttu-id="b33d0-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="b33d0-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="b33d0-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b33d0-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="b33d0-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b33d0-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b33d0-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span><span class="sxs-lookup"><span data-stu-id="b33d0-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="b33d0-174">You must be a Pingboard admin to set up single sign on.</span><span class="sxs-lookup"><span data-stu-id="b33d0-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="b33d0-175">From the top menu select **Apps > Integrations**</span><span class="sxs-lookup"><span data-stu-id="b33d0-175">From the top menu select **Apps > Integrations**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/pingboard_integration.png)

9.  <span data-ttu-id="b33d0-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span><span class="sxs-lookup"><span data-stu-id="b33d0-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/pingboard_aad.png)

10. <span data-ttu-id="b33d0-179">In the modal that follows click **"Configure"**</span><span class="sxs-lookup"><span data-stu-id="b33d0-179">In the modal that follows click **"Configure"**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/pingboard_configure.png)

11. <span data-ttu-id="b33d0-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span><span class="sxs-lookup"><span data-stu-id="b33d0-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="b33d0-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/pingboard_sso_configure.png)

12. <span data-ttu-id="b33d0-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span><span class="sxs-lookup"><span data-stu-id="b33d0-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b33d0-185">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b33d0-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b33d0-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="b33d0-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b33d0-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b33d0-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b33d0-191">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="b33d0-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b33d0-193">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="b33d0-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b33d0-195">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b33d0-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b33d0-197">a.</span><span class="sxs-lookup"><span data-stu-id="b33d0-197">a.</span></span> <span data-ttu-id="b33d0-198">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b33d0-199">b.</span><span class="sxs-lookup"><span data-stu-id="b33d0-199">b.</span></span> <span data-ttu-id="b33d0-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b33d0-201">c.</span><span class="sxs-lookup"><span data-stu-id="b33d0-201">c.</span></span> <span data-ttu-id="b33d0-202">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b33d0-203">d.</span><span class="sxs-lookup"><span data-stu-id="b33d0-203">d.</span></span> <span data-ttu-id="b33d0-204">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="b33d0-205">Creating a Pingboard test user</span><span class="sxs-lookup"><span data-stu-id="b33d0-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="b33d0-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span><span class="sxs-lookup"><span data-stu-id="b33d0-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="b33d0-207">In the case of Pingboard, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b33d0-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="b33d0-208">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b33d0-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b33d0-209">Log in to your Pingboard company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b33d0-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="b33d0-210">Click **“Add Employee”** button on **Directory** page.</span><span class="sxs-lookup"><span data-stu-id="b33d0-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="b33d0-212">On the **“Add Employee”** dialog page, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="b33d0-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_testuser_name.png)

    <span data-ttu-id="b33d0-214">a.</span><span class="sxs-lookup"><span data-stu-id="b33d0-214">a.</span></span> <span data-ttu-id="b33d0-215">In the **Full Name** textbox, type the full name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="b33d0-216">b.</span><span class="sxs-lookup"><span data-stu-id="b33d0-216">b.</span></span> <span data-ttu-id="b33d0-217">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="b33d0-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="b33d0-218">c.</span><span class="sxs-lookup"><span data-stu-id="b33d0-218">c.</span></span> <span data-ttu-id="b33d0-219">In the **Job Title** textbox, type the job title of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="b33d0-220">d.</span><span class="sxs-lookup"><span data-stu-id="b33d0-220">d.</span></span> <span data-ttu-id="b33d0-221">In the **Location** dropdown, select the location  of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b33d0-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="b33d0-222">e.</span><span class="sxs-lookup"><span data-stu-id="b33d0-222">e.</span></span> <span data-ttu-id="b33d0-223">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-223">Click **Add**.</span></span>   

4. <span data-ttu-id="b33d0-224">A confirmation screen will come up to confirm the addition of user.</span><span class="sxs-lookup"><span data-stu-id="b33d0-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![confirm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="b33d0-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="b33d0-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b33d0-227">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b33d0-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b33d0-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span><span class="sxs-lookup"><span data-stu-id="b33d0-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Assign User][200] 

<span data-ttu-id="b33d0-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b33d0-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="b33d0-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b33d0-233">In the applications list, select **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-233">In the applications list, select **Pingboard**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="b33d0-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b33d0-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="b33d0-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b33d0-237">Click **Add** button.</span></span> <span data-ttu-id="b33d0-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b33d0-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="b33d0-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b33d0-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b33d0-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b33d0-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b33d0-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b33d0-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b33d0-243">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="b33d0-243">Testing single sign-on</span></span>

<span data-ttu-id="b33d0-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b33d0-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b33d0-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span><span class="sxs-lookup"><span data-stu-id="b33d0-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b33d0-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b33d0-246">Additional resources</span></span>

* [<span data-ttu-id="b33d0-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b33d0-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b33d0-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b33d0-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-PingBoard-tutorial/tutorial_general_203.png




























