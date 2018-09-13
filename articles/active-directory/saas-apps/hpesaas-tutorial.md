---
title: 'Tutorial: Azure Active Directory integration with HPE SaaS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HPE SaaS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: c8932714f9a9ebcbda82177be2fde37497f71d7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865968"
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="602e9-103">Tutorial: Azure Active Directory integration with HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="602e9-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="602e9-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="602e9-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="602e9-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="602e9-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="602e9-106">You can control in Azure AD who has access to HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="602e9-106">You can control in Azure AD who has access to HPE SaaS</span></span>
- <span data-ttu-id="602e9-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="602e9-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="602e9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="602e9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="602e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="602e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="602e9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="602e9-110">Prerequisites</span></span>

<span data-ttu-id="602e9-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="602e9-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

- <span data-ttu-id="602e9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="602e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="602e9-113">An HPE SaaS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="602e9-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="602e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="602e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="602e9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="602e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="602e9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="602e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="602e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="602e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="602e9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="602e9-118">Scenario description</span></span>
<span data-ttu-id="602e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="602e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="602e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="602e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="602e9-121">Adding HPE SaaS from the gallery</span><span class="sxs-lookup"><span data-stu-id="602e9-121">Adding HPE SaaS from the gallery</span></span>
1. <span data-ttu-id="602e9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="602e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="602e9-123">Adding HPE SaaS from the gallery</span><span class="sxs-lookup"><span data-stu-id="602e9-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="602e9-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="602e9-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="602e9-125">**To add HPE SaaS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="602e9-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="602e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="602e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="602e9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="602e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="602e9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="602e9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="602e9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="602e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="602e9-133">In the search box, type **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="602e9-133">In the search box, type **HPE SaaS**.</span></span>

    ![Creating an Azure AD test user](./media/hpesaas-tutorial/tutorial_hpesaas_search.png)

1. <span data-ttu-id="602e9-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="602e9-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="602e9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="602e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="602e9-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="602e9-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="602e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="602e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span></span> <span data-ttu-id="602e9-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="602e9-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>

<span data-ttu-id="602e9-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="602e9-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="602e9-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="602e9-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="602e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="602e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="602e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="602e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="602e9-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="602e9-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="602e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="602e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="602e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="602e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="602e9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="602e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="602e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span><span class="sxs-lookup"><span data-stu-id="602e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="602e9-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="602e9-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="602e9-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="602e9-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="602e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="602e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

1. <span data-ttu-id="602e9-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="602e9-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="602e9-157">a.</span><span class="sxs-lookup"><span data-stu-id="602e9-157">a.</span></span> <span data-ttu-id="602e9-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="602e9-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="602e9-159">b.</span><span class="sxs-lookup"><span data-stu-id="602e9-159">b.</span></span> <span data-ttu-id="602e9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="602e9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="602e9-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="602e9-161">These values are not real.</span></span> <span data-ttu-id="602e9-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="602e9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="602e9-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="602e9-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span></span> 
 
1. <span data-ttu-id="602e9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="602e9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

1. <span data-ttu-id="602e9-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="602e9-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/hpesaas-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="602e9-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="602e9-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="602e9-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="602e9-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="602e9-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="602e9-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="602e9-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="602e9-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="602e9-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="602e9-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="602e9-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="602e9-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="602e9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="602e9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="602e9-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="602e9-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="602e9-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="602e9-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/hpesaas-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="602e9-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="602e9-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/hpesaas-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="602e9-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="602e9-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/hpesaas-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="602e9-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="602e9-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="602e9-185">a.</span><span class="sxs-lookup"><span data-stu-id="602e9-185">a.</span></span> <span data-ttu-id="602e9-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="602e9-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="602e9-187">b.</span><span class="sxs-lookup"><span data-stu-id="602e9-187">b.</span></span> <span data-ttu-id="602e9-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="602e9-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="602e9-189">c.</span><span class="sxs-lookup"><span data-stu-id="602e9-189">c.</span></span> <span data-ttu-id="602e9-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="602e9-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="602e9-191">d.</span><span class="sxs-lookup"><span data-stu-id="602e9-191">d.</span></span> <span data-ttu-id="602e9-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="602e9-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="602e9-193">Creating an HPE SaaS test user</span><span class="sxs-lookup"><span data-stu-id="602e9-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="602e9-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="602e9-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="602e9-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span><span class="sxs-lookup"><span data-stu-id="602e9-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="602e9-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="602e9-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="602e9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="602e9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span></span>

![Assign User][200] 

<span data-ttu-id="602e9-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="602e9-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="602e9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="602e9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="602e9-202">In the applications list, select **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="602e9-202">In the applications list, select **HPE SaaS**.</span></span>

    ![Configure Single Sign-On](./media/hpesaas-tutorial/tutorial_hpesaas_app.png) 

1. <span data-ttu-id="602e9-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="602e9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="602e9-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="602e9-206">Click **Add** button.</span></span> <span data-ttu-id="602e9-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="602e9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="602e9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="602e9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="602e9-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="602e9-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="602e9-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="602e9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="602e9-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="602e9-212">Testing single sign-on</span></span>

<span data-ttu-id="602e9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="602e9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="602e9-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span><span class="sxs-lookup"><span data-stu-id="602e9-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>
<span data-ttu-id="602e9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="602e9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="602e9-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="602e9-216">Additional resources</span></span>

* [<span data-ttu-id="602e9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="602e9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="602e9-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="602e9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/hpesaas-tutorial/tutorial_general_203.png

