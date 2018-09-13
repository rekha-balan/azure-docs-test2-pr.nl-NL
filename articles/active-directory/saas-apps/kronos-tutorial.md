---
title: 'Tutorial: Azure Active Directory integration with Kronos | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 31e8c990e39b3dc99ccd4dcda0a8d00ecb83b440
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968158"
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="542e4-103">Tutorial: Azure Active Directory integration with Kronos</span><span class="sxs-lookup"><span data-stu-id="542e4-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="542e4-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="542e4-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="542e4-105">Integrating Kronos with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="542e4-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="542e4-106">You can control in Azure AD who has access to Kronos</span><span class="sxs-lookup"><span data-stu-id="542e4-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="542e4-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="542e4-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="542e4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="542e4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="542e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="542e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="542e4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="542e4-110">Prerequisites</span></span>

<span data-ttu-id="542e4-111">To configure Azure AD integration with Kronos, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="542e4-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="542e4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="542e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="542e4-113">A **Kronos Workforce Central** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="542e4-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="542e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="542e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="542e4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="542e4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="542e4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="542e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="542e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="542e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="542e4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="542e4-118">Scenario description</span></span>
<span data-ttu-id="542e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="542e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="542e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="542e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="542e4-121">Adding Kronos from the gallery</span><span class="sxs-lookup"><span data-stu-id="542e4-121">Adding Kronos from the gallery</span></span>
1. <span data-ttu-id="542e4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="542e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="542e4-123">Adding Kronos from the gallery</span><span class="sxs-lookup"><span data-stu-id="542e4-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="542e4-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="542e4-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="542e4-125">**To add Kronos from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="542e4-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="542e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="542e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="542e4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="542e4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="542e4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="542e4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="542e4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="542e4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="542e4-133">In the search box, type **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="542e4-133">In the search box, type **Kronos**.</span></span>

    ![Creating an Azure AD test user](./media/kronos-tutorial/tutorial_kronos_search.png)

1. <span data-ttu-id="542e4-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="542e4-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="542e4-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="542e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="542e4-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="542e4-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="542e4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="542e4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="542e4-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span><span class="sxs-lookup"><span data-stu-id="542e4-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="542e4-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="542e4-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="542e4-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="542e4-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="542e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="542e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="542e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="542e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="542e4-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="542e4-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="542e4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="542e4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="542e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="542e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="542e4-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="542e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="542e4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span><span class="sxs-lookup"><span data-stu-id="542e4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="542e4-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="542e4-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="542e4-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="542e4-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="542e4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="542e4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_kronos_samlbase.png)

1. <span data-ttu-id="542e4-155">On the **Kronos Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="542e4-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="542e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="542e4-157">a.</span></span> <span data-ttu-id="542e4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="542e4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="542e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="542e4-159">b.</span></span> <span data-ttu-id="542e4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="542e4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="542e4-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="542e4-161">These values are not real.</span></span> <span data-ttu-id="542e4-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="542e4-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="542e4-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span><span class="sxs-lookup"><span data-stu-id="542e4-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
1. <span data-ttu-id="542e4-164">Your Kronos application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="542e4-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="542e4-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span><span class="sxs-lookup"><span data-stu-id="542e4-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="542e4-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span><span class="sxs-lookup"><span data-stu-id="542e4-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="542e4-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span><span class="sxs-lookup"><span data-stu-id="542e4-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="542e4-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="542e4-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="542e4-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="542e4-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="542e4-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="542e4-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="542e4-171">This gives the prefix value of email of the user which is the unique User ID.</span><span class="sxs-lookup"><span data-stu-id="542e4-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="542e4-172">This is sent to the Kronos application in every successful response.</span><span class="sxs-lookup"><span data-stu-id="542e4-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_kronos_attribute.png)

1. <span data-ttu-id="542e4-174">In the **User Attributes** section on the **Single sign-on** dialog:</span><span class="sxs-lookup"><span data-stu-id="542e4-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="542e4-175">a.</span><span class="sxs-lookup"><span data-stu-id="542e4-175">a.</span></span> <span data-ttu-id="542e4-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="542e4-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="542e4-177">b.</span><span class="sxs-lookup"><span data-stu-id="542e4-177">b.</span></span> <span data-ttu-id="542e4-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="542e4-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

1. <span data-ttu-id="542e4-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="542e4-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_kronos_certificate.png) 

1. <span data-ttu-id="542e4-181">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="542e4-181">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="542e4-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="542e4-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="542e4-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="542e4-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="542e4-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="542e4-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="542e4-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="542e4-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="542e4-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="542e4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="542e4-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="542e4-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="542e4-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="542e4-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="542e4-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="542e4-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kronos-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="542e4-193">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="542e4-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kronos-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="542e4-195">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="542e4-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kronos-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="542e4-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="542e4-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="542e4-199">a.</span><span class="sxs-lookup"><span data-stu-id="542e4-199">a.</span></span> <span data-ttu-id="542e4-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="542e4-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="542e4-201">b.</span><span class="sxs-lookup"><span data-stu-id="542e4-201">b.</span></span> <span data-ttu-id="542e4-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="542e4-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="542e4-203">c.</span><span class="sxs-lookup"><span data-stu-id="542e4-203">c.</span></span> <span data-ttu-id="542e4-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="542e4-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="542e4-205">d.</span><span class="sxs-lookup"><span data-stu-id="542e4-205">d.</span></span> <span data-ttu-id="542e4-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="542e4-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="542e4-207">Creating a Kronos test user</span><span class="sxs-lookup"><span data-stu-id="542e4-207">Creating a Kronos test user</span></span>

<span data-ttu-id="542e4-208">In this section, you create a user called Britta Simon in Kronos.</span><span class="sxs-lookup"><span data-stu-id="542e4-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="542e4-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span><span class="sxs-lookup"><span data-stu-id="542e4-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="542e4-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="542e4-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="542e4-211">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="542e4-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="542e4-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span><span class="sxs-lookup"><span data-stu-id="542e4-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Assign User][200] 

<span data-ttu-id="542e4-214">**To assign Britta Simon to Kronos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="542e4-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="542e4-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="542e4-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="542e4-217">In the applications list, select **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="542e4-217">In the applications list, select **Kronos**.</span></span>

    ![Configure Single Sign-On](./media/kronos-tutorial/tutorial_kronos_app.png) 

1. <span data-ttu-id="542e4-219">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="542e4-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="542e4-221">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="542e4-221">Click **Add** button.</span></span> <span data-ttu-id="542e4-222">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="542e4-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="542e4-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="542e4-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="542e4-225">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="542e4-225">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="542e4-226">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="542e4-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="542e4-227">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="542e4-227">Testing single sign-on</span></span>

<span data-ttu-id="542e4-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="542e4-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="542e4-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span><span class="sxs-lookup"><span data-stu-id="542e4-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="542e4-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="542e4-230">Additional resources</span></span>

* [<span data-ttu-id="542e4-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="542e4-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="542e4-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="542e4-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/kronos-tutorial/tutorial_general_01.png
[2]: ./media/kronos-tutorial/tutorial_general_02.png
[3]: ./media/kronos-tutorial/tutorial_general_03.png
[4]: ./media/kronos-tutorial/tutorial_general_04.png

[100]: ./media/kronos-tutorial/tutorial_general_100.png

[200]: ./media/kronos-tutorial/tutorial_general_200.png
[201]: ./media/kronos-tutorial/tutorial_general_201.png
[202]: ./media/kronos-tutorial/tutorial_general_202.png
[203]: ./media/kronos-tutorial/tutorial_general_203.png

