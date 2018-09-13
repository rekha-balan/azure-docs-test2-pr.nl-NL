---
title: 'Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Blackboard Learn - Shibboleth.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 1433d2f20c2b75815bce5164e43ff6a8d36407ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867325"
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="15cb8-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="15cb8-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="15cb8-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15cb8-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15cb8-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="15cb8-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="15cb8-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="15cb8-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="15cb8-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="15cb8-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="15cb8-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="15cb8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="15cb8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="15cb8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15cb8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15cb8-110">Prerequisites</span></span>

<span data-ttu-id="15cb8-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="15cb8-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="15cb8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="15cb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15cb8-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="15cb8-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15cb8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="15cb8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15cb8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="15cb8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15cb8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="15cb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15cb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15cb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15cb8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="15cb8-118">Scenario description</span></span>
<span data-ttu-id="15cb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="15cb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15cb8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="15cb8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15cb8-121">Adding Blackboard Learn - Shibboleth from the gallery</span><span class="sxs-lookup"><span data-stu-id="15cb8-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
1. <span data-ttu-id="15cb8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15cb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="15cb8-123">Adding Blackboard Learn - Shibboleth from the gallery</span><span class="sxs-lookup"><span data-stu-id="15cb8-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="15cb8-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="15cb8-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="15cb8-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15cb8-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="15cb8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="15cb8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="15cb8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="15cb8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="15cb8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="15cb8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="15cb8-133">In the search box, type **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

1. <span data-ttu-id="15cb8-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="15cb8-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="15cb8-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15cb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="15cb8-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="15cb8-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="15cb8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15cb8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="15cb8-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span><span class="sxs-lookup"><span data-stu-id="15cb8-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="15cb8-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="15cb8-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="15cb8-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="15cb8-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="15cb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="15cb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="15cb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15cb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="15cb8-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="15cb8-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="15cb8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15cb8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="15cb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="15cb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="15cb8-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15cb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="15cb8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span><span class="sxs-lookup"><span data-stu-id="15cb8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="15cb8-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15cb8-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="15cb8-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="15cb8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15cb8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

1. <span data-ttu-id="15cb8-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15cb8-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="15cb8-157">a.</span><span class="sxs-lookup"><span data-stu-id="15cb8-157">a.</span></span> <span data-ttu-id="15cb8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="15cb8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="15cb8-159">b.</span><span class="sxs-lookup"><span data-stu-id="15cb8-159">b.</span></span> <span data-ttu-id="15cb8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="15cb8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="15cb8-161">c.</span><span class="sxs-lookup"><span data-stu-id="15cb8-161">c.</span></span> <span data-ttu-id="15cb8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="15cb8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="15cb8-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="15cb8-163">These values are not real.</span></span> <span data-ttu-id="15cb8-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="15cb8-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="15cb8-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span><span class="sxs-lookup"><span data-stu-id="15cb8-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

1. <span data-ttu-id="15cb8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="15cb8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

1. <span data-ttu-id="15cb8-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="15cb8-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="15cb8-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="15cb8-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="15cb8-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="15cb8-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

1. <span data-ttu-id="15cb8-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cb8-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="15cb8-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="15cb8-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="15cb8-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="15cb8-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="15cb8-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15cb8-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="15cb8-177">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15cb8-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="15cb8-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15cb8-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="15cb8-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15cb8-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="15cb8-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="15cb8-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="15cb8-183">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="15cb8-185">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="15cb8-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="15cb8-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15cb8-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15cb8-189">a.</span><span class="sxs-lookup"><span data-stu-id="15cb8-189">a.</span></span> <span data-ttu-id="15cb8-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15cb8-191">b.</span><span class="sxs-lookup"><span data-stu-id="15cb8-191">b.</span></span> <span data-ttu-id="15cb8-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="15cb8-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="15cb8-193">c.</span><span class="sxs-lookup"><span data-stu-id="15cb8-193">c.</span></span> <span data-ttu-id="15cb8-194">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="15cb8-195">d.</span><span class="sxs-lookup"><span data-stu-id="15cb8-195">d.</span></span> <span data-ttu-id="15cb8-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="15cb8-197">Creating a Blackboard Learn - Shibboleth test user</span><span class="sxs-lookup"><span data-stu-id="15cb8-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="15cb8-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="15cb8-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="15cb8-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span><span class="sxs-lookup"><span data-stu-id="15cb8-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="15cb8-200">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15cb8-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="15cb8-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="15cb8-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Assign User][200] 

<span data-ttu-id="15cb8-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15cb8-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="15cb8-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="15cb8-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

1. <span data-ttu-id="15cb8-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="15cb8-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="15cb8-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="15cb8-210">Click **Add** button.</span></span> <span data-ttu-id="15cb8-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15cb8-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="15cb8-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="15cb8-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="15cb8-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="15cb8-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="15cb8-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15cb8-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="15cb8-216">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="15cb8-216">Testing single sign-on</span></span>

<span data-ttu-id="15cb8-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="15cb8-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="15cb8-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span><span class="sxs-lookup"><span data-stu-id="15cb8-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15cb8-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="15cb8-219">Additional resources</span></span>

* [<span data-ttu-id="15cb8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15cb8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="15cb8-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="15cb8-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

