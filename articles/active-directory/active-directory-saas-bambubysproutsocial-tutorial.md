---
title: 'Tutorial: Azure Active Directory integration with Bambu by Sprout Social | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bambu by Sprout Social.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: ececa817851cf72afb444688ab59ba6584d0c951
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564046"
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="3d342-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="3d342-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="3d342-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d342-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d342-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3d342-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d342-106">You can control in Azure AD who has access to Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="3d342-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="3d342-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3d342-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d342-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3d342-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d342-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d342-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="3d342-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3d342-110">Prerequisites</span></span>

<span data-ttu-id="3d342-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3d342-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="3d342-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3d342-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d342-113">A Bambu by Sprout Social single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3d342-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d342-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3d342-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d342-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3d342-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d342-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3d342-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3d342-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d342-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d342-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3d342-118">Scenario description</span></span>
<span data-ttu-id="3d342-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3d342-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d342-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3d342-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d342-121">Adding Bambu by Sprout Social from the gallery</span><span class="sxs-lookup"><span data-stu-id="3d342-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="3d342-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d342-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="3d342-123">Adding Bambu by Sprout Social from the gallery</span><span class="sxs-lookup"><span data-stu-id="3d342-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="3d342-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3d342-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d342-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d342-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d342-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3d342-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d342-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3d342-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d342-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d342-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3d342-131">Click **New application** button on the top of the dialog to add new application.</span><span class="sxs-lookup"><span data-stu-id="3d342-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3d342-133">In the search box, type **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="3d342-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="3d342-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3d342-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d342-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d342-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d342-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d342-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d342-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d342-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="3d342-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3d342-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="3d342-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="3d342-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="3d342-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3d342-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d342-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3d342-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d342-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d342-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d342-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3d342-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3d342-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d342-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d342-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3d342-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d342-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d342-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d342-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span><span class="sxs-lookup"><span data-stu-id="3d342-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="3d342-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d342-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="3d342-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3d342-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="3d342-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="3d342-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="3d342-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="3d342-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="3d342-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3d342-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="3d342-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3d342-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d342-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3d342-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3d342-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3d342-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="3d342-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="3d342-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="3d342-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="3d342-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3d342-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3d342-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d342-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3d342-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d342-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d342-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d342-169">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d342-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d342-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d342-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="3d342-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d342-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d342-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3d342-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d342-175">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="3d342-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d342-177">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d342-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d342-179">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d342-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d342-181">a.</span><span class="sxs-lookup"><span data-stu-id="3d342-181">a.</span></span> <span data-ttu-id="3d342-182">In the **Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3d342-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3d342-183">b.</span><span class="sxs-lookup"><span data-stu-id="3d342-183">b.</span></span> <span data-ttu-id="3d342-184">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d342-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3d342-185">c.</span><span class="sxs-lookup"><span data-stu-id="3d342-185">c.</span></span> <span data-ttu-id="3d342-186">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="3d342-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d342-187">d.</span><span class="sxs-lookup"><span data-stu-id="3d342-187">d.</span></span> <span data-ttu-id="3d342-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d342-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="3d342-189">Creating a Bambu by Sprout Social test user</span><span class="sxs-lookup"><span data-stu-id="3d342-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="3d342-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="3d342-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d342-191">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d342-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d342-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="3d342-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Assign User][200] 

<span data-ttu-id="3d342-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3d342-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="3d342-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d342-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3d342-197">In the applications list, select **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="3d342-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="3d342-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3d342-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="3d342-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3d342-201">Click **Add** button.</span></span> <span data-ttu-id="3d342-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d342-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="3d342-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3d342-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d342-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d342-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d342-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3d342-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d342-207">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d342-207">Testing single sign-on</span></span>

<span data-ttu-id="3d342-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3d342-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d342-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span><span class="sxs-lookup"><span data-stu-id="3d342-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="3d342-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3d342-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3d342-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3d342-211">Additional resources</span></span>

* [<span data-ttu-id="3d342-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d342-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d342-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d342-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png






















