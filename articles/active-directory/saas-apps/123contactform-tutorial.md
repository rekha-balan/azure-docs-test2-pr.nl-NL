---
title: 'Tutorial: Azure Active Directory integration with 123ContactForm | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ecbe627697fc4f8b5fbfecf96c3cb65d9ffe4607
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868936"
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="9550c-103">Tutorial: Azure Active Directory integration with 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="9550c-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="9550c-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9550c-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9550c-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9550c-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9550c-106">You can control in Azure AD who has access to 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="9550c-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="9550c-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9550c-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9550c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9550c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9550c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9550c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9550c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9550c-110">Prerequisites</span></span>

<span data-ttu-id="9550c-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9550c-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="9550c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9550c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9550c-113">A 123ContactForm single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9550c-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9550c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9550c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9550c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9550c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9550c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9550c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9550c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9550c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9550c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9550c-118">Scenario description</span></span>
<span data-ttu-id="9550c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9550c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9550c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9550c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9550c-121">Adding 123ContactForm from the gallery</span><span class="sxs-lookup"><span data-stu-id="9550c-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="9550c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9550c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="9550c-123">Adding 123ContactForm from the gallery</span><span class="sxs-lookup"><span data-stu-id="9550c-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="9550c-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9550c-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9550c-125">**To add 123ContactForm from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9550c-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9550c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9550c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9550c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9550c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9550c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9550c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9550c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9550c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9550c-133">In the search box, type **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="9550c-133">In the search box, type **123ContactForm**.</span></span>

    ![Creating an Azure AD test user](./media/123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="9550c-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9550c-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9550c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9550c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9550c-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9550c-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9550c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9550c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="9550c-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9550c-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="9550c-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9550c-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9550c-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9550c-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9550c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9550c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9550c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9550c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9550c-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9550c-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9550c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9550c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9550c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9550c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9550c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9550c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9550c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span><span class="sxs-lookup"><span data-stu-id="9550c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="9550c-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9550c-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="9550c-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9550c-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="9550c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9550c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="9550c-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9550c-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/url1.png)

    <span data-ttu-id="9550c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9550c-157">a.</span></span> <span data-ttu-id="9550c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="9550c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="9550c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9550c-159">b.</span></span> <span data-ttu-id="9550c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="9550c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="9550c-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9550c-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/url2.png)

    <span data-ttu-id="9550c-163">a.</span><span class="sxs-lookup"><span data-stu-id="9550c-163">a.</span></span> <span data-ttu-id="9550c-164">Click the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="9550c-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="9550c-165">b.</span><span class="sxs-lookup"><span data-stu-id="9550c-165">b.</span></span> <span data-ttu-id="9550c-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="9550c-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9550c-167">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9550c-167">These values are not real.</span></span> <span data-ttu-id="9550c-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="9550c-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="9550c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9550c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="9550c-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9550c-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9550c-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9550c-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/submit.png) 

    <span data-ttu-id="9550c-175">a.</span><span class="sxs-lookup"><span data-stu-id="9550c-175">a.</span></span> <span data-ttu-id="9550c-176">In the **Email** textbox, type the email of the user i.e</span><span class="sxs-lookup"><span data-stu-id="9550c-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="9550c-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9550c-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="9550c-178">b.</span><span class="sxs-lookup"><span data-stu-id="9550c-178">b.</span></span> <span data-ttu-id="9550c-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9550c-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="9550c-180">c.</span><span class="sxs-lookup"><span data-stu-id="9550c-180">c.</span></span> <span data-ttu-id="9550c-181">Click **SUBMIT FORM**.</span><span class="sxs-lookup"><span data-stu-id="9550c-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="9550c-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9550c-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/123contactform-tutorial/url3.png)

    <span data-ttu-id="9550c-184">a.</span><span class="sxs-lookup"><span data-stu-id="9550c-184">a.</span></span> <span data-ttu-id="9550c-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9550c-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="9550c-186">b.</span><span class="sxs-lookup"><span data-stu-id="9550c-186">b.</span></span> <span data-ttu-id="9550c-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9550c-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="9550c-188">c.</span><span class="sxs-lookup"><span data-stu-id="9550c-188">c.</span></span> <span data-ttu-id="9550c-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9550c-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="9550c-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9550c-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9550c-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9550c-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9550c-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9550c-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9550c-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9550c-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9550c-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9550c-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9550c-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9550c-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9550c-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9550c-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9550c-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9550c-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9550c-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9550c-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9550c-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9550c-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9550c-205">a.</span><span class="sxs-lookup"><span data-stu-id="9550c-205">a.</span></span> <span data-ttu-id="9550c-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9550c-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9550c-207">b.</span><span class="sxs-lookup"><span data-stu-id="9550c-207">b.</span></span> <span data-ttu-id="9550c-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9550c-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9550c-209">c.</span><span class="sxs-lookup"><span data-stu-id="9550c-209">c.</span></span> <span data-ttu-id="9550c-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9550c-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9550c-211">d.</span><span class="sxs-lookup"><span data-stu-id="9550c-211">d.</span></span> <span data-ttu-id="9550c-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9550c-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="9550c-213">Creating a 123ContactForm test user</span><span class="sxs-lookup"><span data-stu-id="9550c-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="9550c-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="9550c-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9550c-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9550c-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9550c-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9550c-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Assign User][200] 

<span data-ttu-id="9550c-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9550c-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="9550c-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9550c-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="9550c-221">In the applications list, select **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="9550c-221">In the applications list, select **123ContactForm**.</span></span>

    ![Configure Single Sign-On](./media/123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="9550c-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9550c-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="9550c-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9550c-225">Click **Add** button.</span></span> <span data-ttu-id="9550c-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9550c-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="9550c-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9550c-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9550c-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9550c-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9550c-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9550c-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9550c-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9550c-231">Testing single sign-on</span></span>

<span data-ttu-id="9550c-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9550c-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9550c-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span><span class="sxs-lookup"><span data-stu-id="9550c-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="9550c-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9550c-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9550c-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9550c-235">Additional resources</span></span>

* [<span data-ttu-id="9550c-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9550c-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9550c-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9550c-237">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/123contactform-tutorial/tutorial_general_01.png
[2]: ./media/123contactform-tutorial/tutorial_general_02.png
[3]: ./media/123contactform-tutorial/tutorial_general_03.png
[4]: ./media/123contactform-tutorial/tutorial_general_04.png

[100]: ./media/123contactform-tutorial/tutorial_general_100.png

[200]: ./media/123contactform-tutorial/tutorial_general_200.png
[201]: ./media/123contactform-tutorial/tutorial_general_201.png
[202]: ./media/123contactform-tutorial/tutorial_general_202.png
[203]: ./media/123contactform-tutorial/tutorial_general_203.png

