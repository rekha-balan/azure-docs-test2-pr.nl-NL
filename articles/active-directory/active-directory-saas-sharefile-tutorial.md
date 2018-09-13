---
title: 'Tutorial: Azure Active Directory integration with Citrix ShareFile | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ddf6c69b-4a76-4b42-8619-6f2a22800a23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 753a00e9e51aa2add5434b2d33f44f7d4e779d29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553828"
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="2d330-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="2d330-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="2d330-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d330-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d330-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2d330-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d330-106">You can control in Azure AD who has access to Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="2d330-106">You can control in Azure AD who has access to Citrix ShareFile</span></span>
- <span data-ttu-id="2d330-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2d330-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d330-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="2d330-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2d330-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d330-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d330-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d330-110">Prerequisites</span></span>

<span data-ttu-id="2d330-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2d330-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="2d330-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2d330-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d330-113">A Citrix ShareFile single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2d330-113">A Citrix ShareFile single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2d330-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2d330-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2d330-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2d330-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d330-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="2d330-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2d330-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d330-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2d330-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2d330-118">Scenario description</span></span>
<span data-ttu-id="2d330-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2d330-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d330-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2d330-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d330-121">Adding Citrix ShareFile from the gallery</span><span class="sxs-lookup"><span data-stu-id="2d330-121">Adding Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="2d330-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d330-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="2d330-123">Adding Citrix ShareFile from the gallery</span><span class="sxs-lookup"><span data-stu-id="2d330-123">Adding Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="2d330-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2d330-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d330-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d330-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d330-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2d330-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d330-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2d330-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d330-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2d330-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2d330-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2d330-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2d330-133">In the search box, type **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="2d330-133">In the search box, type **Citrix ShareFile**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_001.png)

5. <span data-ttu-id="2d330-135">In the results panel, select **Citrix ShareFile**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2d330-135">In the results panel, select **Citrix ShareFile**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d330-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d330-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d330-138">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d330-138">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d330-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d330-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="2d330-140">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2d330-140">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="2d330-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2d330-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix ShareFile.</span></span>

<span data-ttu-id="2d330-142">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2d330-142">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d330-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2d330-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2d330-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d330-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d330-145">**[Creating a Citrix ShareFile test user](#creating-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="2d330-145">**[Creating a Citrix ShareFile test user](#creating-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2d330-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d330-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d330-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2d330-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d330-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d330-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d330-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Citrix ShareFile application.</span><span class="sxs-lookup"><span data-stu-id="2d330-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="2d330-150">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d330-150">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="2d330-151">In the Azure Management portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2d330-151">In the Azure Management portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="2d330-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="2d330-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_01.png)

3. <span data-ttu-id="2d330-155">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d330-155">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_02.png)

    <span data-ttu-id="2d330-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d330-157">a.</span></span> <span data-ttu-id="2d330-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="2d330-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="2d330-159">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="2d330-159">Please note that these are not the real values.</span></span> <span data-ttu-id="2d330-160">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="2d330-160">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="2d330-161">If you don't know about these URLs, type sample URLs with example pattern and then you will get the actual URLs after you complete step 13.</span><span class="sxs-lookup"><span data-stu-id="2d330-161">If you don't know about these URLs, type sample URLs with example pattern and then you will get the actual URLs after you complete step 13.</span></span>

4. <span data-ttu-id="2d330-162">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2d330-162">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_05.png) 

5. <span data-ttu-id="2d330-164">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2d330-164">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_07.png)

6. <span data-ttu-id="2d330-167">In a different web browser window, log into your Citrix ShareFile company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2d330-167">In a different web browser window, log into your Citrix ShareFile company site as an administrator.</span></span>

7. <span data-ttu-id="2d330-168">In the toolbar on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2d330-168">In the toolbar on the top, click **Admin**.</span></span>

8. <span data-ttu-id="2d330-169">In the left navigation pane, select **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2d330-169">In the left navigation pane, select **Configure Single Sign-On**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_002.png)

9. <span data-ttu-id="2d330-171">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d330-171">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/sso_configuration_2.png)

    <span data-ttu-id="2d330-173">a.</span><span class="sxs-lookup"><span data-stu-id="2d330-173">a.</span></span> <span data-ttu-id="2d330-174">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="2d330-174">Click **Enable SAML**.</span></span>

    <span data-ttu-id="2d330-175">b.</span><span class="sxs-lookup"><span data-stu-id="2d330-175">b.</span></span> <span data-ttu-id="2d330-176">In the **Your IDP Issuer/ Entity ID** textbox, put the value of **SAML Entity ID** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="2d330-176">In the **Your IDP Issuer/ Entity ID** textbox, put the value of **SAML Entity ID** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="2d330-177">c.</span><span class="sxs-lookup"><span data-stu-id="2d330-177">c.</span></span> <span data-ttu-id="2d330-178">Click **Change** next to the **X.509 Certificate** field and then upload your downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="2d330-178">Click **Change** next to the **X.509 Certificate** field and then upload your downloaded certificate file.</span></span> 

    <span data-ttu-id="2d330-179">d.</span><span class="sxs-lookup"><span data-stu-id="2d330-179">d.</span></span> <span data-ttu-id="2d330-180">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="2d330-180">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="2d330-181">e.</span><span class="sxs-lookup"><span data-stu-id="2d330-181">e.</span></span> <span data-ttu-id="2d330-182">In the **Logout URL** textbox, put the value of **Sign-Out URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="2d330-182">In the **Logout URL** textbox, put the value of **Sign-Out URL** from Azure AD application configuration window.</span></span>

10. <span data-ttu-id="2d330-183">Click **Save** on the Citrix ShareFile management portal.</span><span class="sxs-lookup"><span data-stu-id="2d330-183">Click **Save** on the Citrix ShareFile management portal.</span></span>
    
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d330-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2d330-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d330-185">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d330-185">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2d330-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d330-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d330-188">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2d330-188">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d330-190">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="2d330-190">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d330-192">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d330-192">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d330-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d330-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d330-196">a.</span><span class="sxs-lookup"><span data-stu-id="2d330-196">a.</span></span> <span data-ttu-id="2d330-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d330-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d330-198">b.</span><span class="sxs-lookup"><span data-stu-id="2d330-198">b.</span></span> <span data-ttu-id="2d330-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d330-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d330-200">c.</span><span class="sxs-lookup"><span data-stu-id="2d330-200">c.</span></span> <span data-ttu-id="2d330-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2d330-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d330-202">d.</span><span class="sxs-lookup"><span data-stu-id="2d330-202">d.</span></span> <span data-ttu-id="2d330-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d330-203">Click **Create**.</span></span> 



### <a name="creating-a-citrix-sharefile-test-user"></a><span data-ttu-id="2d330-204">Creating a Citrix ShareFile test user</span><span class="sxs-lookup"><span data-stu-id="2d330-204">Creating a Citrix ShareFile test user</span></span>

<span data-ttu-id="2d330-205">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2d330-205">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="2d330-206">In the case of Citrix ShareFile, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="2d330-206">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

####<a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="2d330-207">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d330-207">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="2d330-208">Log into your Citrix ShareFile company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2d330-208">Log into your Citrix ShareFile company site as an administrator.</span></span>

2. <span data-ttu-id="2d330-209">In the toolbar on the top, click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="2d330-209">In the toolbar on the top, click **Manage Users**.</span></span> <span data-ttu-id="2d330-210">Then go to **Manage Users Home** and click **Create Employee**.</span><span class="sxs-lookup"><span data-stu-id="2d330-210">Then go to **Manage Users Home** and click **Create Employee**.</span></span>

    <span data-ttu-id="2d330-211">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_010.png "New User")</span><span class="sxs-lookup"><span data-stu-id="2d330-211">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_010.png "New User")</span></span>

3. <span data-ttu-id="2d330-212">On the **Basic Information** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="2d330-212">On the **Basic Information** section, perform below steps:</span></span>

    <span data-ttu-id="2d330-213">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_011.png "New User")</span><span class="sxs-lookup"><span data-stu-id="2d330-213">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_011.png "New User")</span></span>

    <span data-ttu-id="2d330-214">a.</span><span class="sxs-lookup"><span data-stu-id="2d330-214">a.</span></span> <span data-ttu-id="2d330-215">In the **Email Address** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="2d330-215">In the **Email Address** textbox, type the email address of Britta Simon account.</span></span>  

    <span data-ttu-id="2d330-216">b.</span><span class="sxs-lookup"><span data-stu-id="2d330-216">b.</span></span> <span data-ttu-id="2d330-217">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2d330-217">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="2d330-218">c.</span><span class="sxs-lookup"><span data-stu-id="2d330-218">c.</span></span> <span data-ttu-id="2d330-219">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d330-219">In the **Last Name** textbox, type **Simon**.</span></span>

4. <span data-ttu-id="2d330-220">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2d330-220">Click **Add User**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2d330-221">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="2d330-221">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="2d330-222">You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="2d330-222">You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision AAD user accounts.</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2d330-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2d330-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2d330-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="2d330-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Citrix ShareFile.</span></span>

![Assign User][200] 

<span data-ttu-id="2d330-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d330-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="2d330-227">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2d330-227">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="2d330-229">In the applications list, select **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="2d330-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_50.png) 

3. <span data-ttu-id="2d330-231">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2d330-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="2d330-233">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2d330-233">Click **Add** button.</span></span> <span data-ttu-id="2d330-234">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d330-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="2d330-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2d330-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2d330-237">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d330-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d330-238">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d330-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2d330-239">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d330-239">Testing single sign-on</span></span>

<span data-ttu-id="2d330-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2d330-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2d330-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span><span class="sxs-lookup"><span data-stu-id="2d330-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2d330-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2d330-242">Additional resources</span></span>

* [<span data-ttu-id="2d330-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d330-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d330-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d330-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png
























