---
title: 'Tutorial: Azure Active Directory integration with Teamphoria | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: a973923894ed743fcba5ca4f208389f232a6c180
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670258"
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="af7a1-103">Tutorial: Azure Active Directory integration with Teamphoria</span><span class="sxs-lookup"><span data-stu-id="af7a1-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="af7a1-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af7a1-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af7a1-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="af7a1-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="af7a1-106">You can control in Azure AD who has access to Teamphoria</span><span class="sxs-lookup"><span data-stu-id="af7a1-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="af7a1-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="af7a1-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af7a1-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="af7a1-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="af7a1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af7a1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="af7a1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af7a1-110">Prerequisites</span></span>

<span data-ttu-id="af7a1-111">To configure Azure AD integration with Teamphoria, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="af7a1-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="af7a1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="af7a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af7a1-113">A Teamphoria single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="af7a1-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af7a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="af7a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af7a1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="af7a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af7a1-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="af7a1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="af7a1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af7a1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af7a1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="af7a1-118">Scenario description</span></span>
<span data-ttu-id="af7a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="af7a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af7a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="af7a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af7a1-121">Adding Teamphoria from the gallery</span><span class="sxs-lookup"><span data-stu-id="af7a1-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="af7a1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="af7a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="af7a1-123">Adding Teamphoria from the gallery</span><span class="sxs-lookup"><span data-stu-id="af7a1-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="af7a1-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="af7a1-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af7a1-125">**To add Teamphoria from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af7a1-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af7a1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="af7a1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="af7a1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="af7a1-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="af7a1-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="af7a1-133">In the search box, type **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-133">In the search box, type **Teamphoria**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="af7a1-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="af7a1-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af7a1-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="af7a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="af7a1-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af7a1-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af7a1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af7a1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="af7a1-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span><span class="sxs-lookup"><span data-stu-id="af7a1-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="af7a1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="af7a1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="af7a1-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="af7a1-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af7a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="af7a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af7a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af7a1-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="af7a1-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="af7a1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af7a1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af7a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="af7a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af7a1-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="af7a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af7a1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span><span class="sxs-lookup"><span data-stu-id="af7a1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="af7a1-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af7a1-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="af7a1-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="af7a1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="af7a1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="af7a1-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af7a1-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="af7a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="af7a1-157">a.</span></span> <span data-ttu-id="af7a1-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="af7a1-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="af7a1-159">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="af7a1-159">Please note that these are not the real values.</span></span> <span data-ttu-id="af7a1-160">You have to update these values with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="af7a1-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="af7a1-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="af7a1-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="af7a1-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span><span class="sxs-lookup"><span data-stu-id="af7a1-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="af7a1-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="af7a1-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af7a1-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="af7a1-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="af7a1-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="af7a1-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="af7a1-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="af7a1-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="af7a1-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span><span class="sxs-lookup"><span data-stu-id="af7a1-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="af7a1-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span><span class="sxs-lookup"><span data-stu-id="af7a1-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="af7a1-174">Enter the details in the fields as described below-</span><span class="sxs-lookup"><span data-stu-id="af7a1-174">Enter the details in the fields as described below-</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/teamphoria_sso_save.png)

    <span data-ttu-id="af7a1-176">a.</span><span class="sxs-lookup"><span data-stu-id="af7a1-176">a.</span></span> <span data-ttu-id="af7a1-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span><span class="sxs-lookup"><span data-stu-id="af7a1-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="af7a1-178">b.</span><span class="sxs-lookup"><span data-stu-id="af7a1-178">b.</span></span> <span data-ttu-id="af7a1-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span><span class="sxs-lookup"><span data-stu-id="af7a1-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="af7a1-180">c.</span><span class="sxs-lookup"><span data-stu-id="af7a1-180">c.</span></span> <span data-ttu-id="af7a1-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span><span class="sxs-lookup"><span data-stu-id="af7a1-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="af7a1-182">d.</span><span class="sxs-lookup"><span data-stu-id="af7a1-182">d.</span></span> <span data-ttu-id="af7a1-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="af7a1-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="af7a1-184">e.</span><span class="sxs-lookup"><span data-stu-id="af7a1-184">e.</span></span> <span data-ttu-id="af7a1-185">Switch the option to **ON** and click on **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af7a1-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="af7a1-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="af7a1-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="af7a1-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af7a1-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af7a1-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af7a1-192">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="af7a1-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af7a1-194">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="af7a1-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af7a1-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af7a1-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af7a1-198">a.</span><span class="sxs-lookup"><span data-stu-id="af7a1-198">a.</span></span> <span data-ttu-id="af7a1-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af7a1-200">b.</span><span class="sxs-lookup"><span data-stu-id="af7a1-200">b.</span></span> <span data-ttu-id="af7a1-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af7a1-202">c.</span><span class="sxs-lookup"><span data-stu-id="af7a1-202">c.</span></span> <span data-ttu-id="af7a1-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="af7a1-204">d.</span><span class="sxs-lookup"><span data-stu-id="af7a1-204">d.</span></span> <span data-ttu-id="af7a1-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="af7a1-206">Creating a Teamphoria test user</span><span class="sxs-lookup"><span data-stu-id="af7a1-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="af7a1-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="af7a1-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="af7a1-208">In the case of Teamphoria, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="af7a1-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="af7a1-209">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af7a1-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="af7a1-210">Log in to your Teamphoria company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="af7a1-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="af7a1-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span><span class="sxs-lookup"><span data-stu-id="af7a1-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="af7a1-213">Click on the **MANUAL INVITE** option.</span><span class="sxs-lookup"><span data-stu-id="af7a1-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png) 

4. <span data-ttu-id="af7a1-215">On this page, perform following action.</span><span class="sxs-lookup"><span data-stu-id="af7a1-215">On this page, perform following action.</span></span> 
    
    ![Invite People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png) 

    <span data-ttu-id="af7a1-217">a.</span><span class="sxs-lookup"><span data-stu-id="af7a1-217">a.</span></span> <span data-ttu-id="af7a1-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af7a1-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af7a1-219">b.</span><span class="sxs-lookup"><span data-stu-id="af7a1-219">b.</span></span> <span data-ttu-id="af7a1-220">In the **FIRST NAME** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="af7a1-221">c.</span><span class="sxs-lookup"><span data-stu-id="af7a1-221">c.</span></span> <span data-ttu-id="af7a1-222">In the **LAST NAME** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="af7a1-223">d.</span><span class="sxs-lookup"><span data-stu-id="af7a1-223">d.</span></span> <span data-ttu-id="af7a1-224">Click **INVITE 1 USER**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="af7a1-225">User needs to accept the invite to get created in the system.</span><span class="sxs-lookup"><span data-stu-id="af7a1-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="af7a1-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="af7a1-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="af7a1-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="af7a1-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Assign User][200] 

<span data-ttu-id="af7a1-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af7a1-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="af7a1-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="af7a1-232">In the applications list, select **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-232">In the applications list, select **Teamphoria**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="af7a1-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="af7a1-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="af7a1-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="af7a1-236">Click **Add** button.</span></span> <span data-ttu-id="af7a1-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="af7a1-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="af7a1-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="af7a1-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="af7a1-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="af7a1-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af7a1-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="af7a1-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af7a1-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="af7a1-242">Testing single sign-on</span></span>

<span data-ttu-id="af7a1-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="af7a1-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="af7a1-244">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="af7a1-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="af7a1-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="af7a1-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="af7a1-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="af7a1-246">Additional resources</span></span>

* [<span data-ttu-id="af7a1-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af7a1-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af7a1-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af7a1-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png




























