---
title: 'Tutorial: Azure Active Directory integration with BitaBIZ | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BitaBIZ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 1a51e677-c62b-4aee-9c61-56926aaaa899
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/15/2017
ms.author: jeedes
ms.openlocfilehash: 2a05a4f1b9162a69e074bf6243236df48c8ce536
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865681"
---
# <a name="tutorial-azure-active-directory-integration-with-bitabiz"></a><span data-ttu-id="9a28c-103">Tutorial: Azure Active Directory integration with BitaBIZ</span><span class="sxs-lookup"><span data-stu-id="9a28c-103">Tutorial: Azure Active Directory integration with BitaBIZ</span></span>

<span data-ttu-id="9a28c-104">In this tutorial, you learn how to integrate BitaBIZ with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a28c-104">In this tutorial, you learn how to integrate BitaBIZ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a28c-105">Integrating BitaBIZ with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9a28c-105">Integrating BitaBIZ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a28c-106">You can control in Azure AD who has access to BitaBIZ.</span><span class="sxs-lookup"><span data-stu-id="9a28c-106">You can control in Azure AD who has access to BitaBIZ.</span></span>
- <span data-ttu-id="9a28c-107">You can enable your users to automatically get signed-on to BitaBIZ (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9a28c-107">You can enable your users to automatically get signed-on to BitaBIZ (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9a28c-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a28c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9a28c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9a28c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a28c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a28c-110">Prerequisites</span></span>

<span data-ttu-id="9a28c-111">To configure Azure AD integration with BitaBIZ, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9a28c-111">To configure Azure AD integration with BitaBIZ, you need the following items:</span></span>

- <span data-ttu-id="9a28c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9a28c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a28c-113">A BitaBIZ single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9a28c-113">A BitaBIZ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a28c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9a28c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a28c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9a28c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a28c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9a28c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a28c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a28c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a28c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9a28c-118">Scenario description</span></span>
<span data-ttu-id="9a28c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9a28c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a28c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9a28c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a28c-121">Adding BitaBIZ from the gallery</span><span class="sxs-lookup"><span data-stu-id="9a28c-121">Adding BitaBIZ from the gallery</span></span>
1. <span data-ttu-id="9a28c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a28c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bitabiz-from-the-gallery"></a><span data-ttu-id="9a28c-123">Adding BitaBIZ from the gallery</span><span class="sxs-lookup"><span data-stu-id="9a28c-123">Adding BitaBIZ from the gallery</span></span>
<span data-ttu-id="9a28c-124">To configure the integration of BitaBIZ into Azure AD, you need to add BitaBIZ from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9a28c-124">To configure the integration of BitaBIZ into Azure AD, you need to add BitaBIZ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a28c-125">**To add BitaBIZ from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a28c-125">**To add BitaBIZ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a28c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9a28c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9a28c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a28c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="9a28c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9a28c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9a28c-133">In the search box, type **BitaBIZ**, select **BitaBIZ** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9a28c-133">In the search box, type **BitaBIZ**, select **BitaBIZ** from result panel then click **Add** button to add the application.</span></span>

    ![BitaBIZ in the results list](./media/bitabiz-tutorial/tutorial_bitabiz_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a28c-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a28c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a28c-136">In this section, you configure and test Azure AD single sign-on with BitaBIZ based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9a28c-136">In this section, you configure and test Azure AD single sign-on with BitaBIZ based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a28c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in BitaBIZ is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a28c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in BitaBIZ is to a user in Azure AD.</span></span> <span data-ttu-id="9a28c-138">In other words, a link relationship between an Azure AD user and the related user in BitaBIZ needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9a28c-138">In other words, a link relationship between an Azure AD user and the related user in BitaBIZ needs to be established.</span></span>

<span data-ttu-id="9a28c-139">In BitaBIZ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9a28c-139">In BitaBIZ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a28c-140">To configure and test Azure AD single sign-on with BitaBIZ, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9a28c-140">To configure and test Azure AD single sign-on with BitaBIZ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a28c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9a28c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9a28c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a28c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9a28c-143">**[Create a BitaBIZ test user](#create-a-bitabiz-test-user)** - to have a counterpart of Britta Simon in BitaBIZ that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9a28c-143">**[Create a BitaBIZ test user](#create-a-bitabiz-test-user)** - to have a counterpart of Britta Simon in BitaBIZ that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9a28c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9a28c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9a28c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9a28c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a28c-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a28c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a28c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BitaBIZ application.</span><span class="sxs-lookup"><span data-stu-id="9a28c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BitaBIZ application.</span></span>

<span data-ttu-id="9a28c-148">**To configure Azure AD single sign-on with BitaBIZ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a28c-148">**To configure Azure AD single sign-on with BitaBIZ, perform the following steps:**</span></span>

1. <span data-ttu-id="9a28c-149">In the Azure portal, on the **BitaBIZ** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-149">In the Azure portal, on the **BitaBIZ** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="9a28c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9a28c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bitabiz-tutorial/tutorial_bitabiz_samlbase.png)

1. <span data-ttu-id="9a28c-153">On the **BitaBIZ Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="9a28c-153">On the **BitaBIZ Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![BitaBIZ Domain and URLs single sign-on information](./media/bitabiz-tutorial/tutorial_bitabiz_url.png)

    <span data-ttu-id="9a28c-155">In the **Identifier** textbox, type a URL using the following pattern: `https://www.bitabiz.com/<instanceId>`</span><span class="sxs-lookup"><span data-stu-id="9a28c-155">In the **Identifier** textbox, type a URL using the following pattern: `https://www.bitabiz.com/<instanceId>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a28c-156">The value in the above URL is for demonstration only.</span><span class="sxs-lookup"><span data-stu-id="9a28c-156">The value in the above URL is for demonstration only.</span></span> <span data-ttu-id="9a28c-157">Update the value with the actual identifier, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a28c-157">Update the value with the actual identifier, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="9a28c-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="9a28c-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![BitaBIZ Domain and URLs single sign-on information](./media/bitabiz-tutorial/tutorial_bitabiz_url1.png)

    <span data-ttu-id="9a28c-160">In the **Sign-on URL** textbox, type the URL: `https://www.bitabiz.com/dashboard`</span><span class="sxs-lookup"><span data-stu-id="9a28c-160">In the **Sign-on URL** textbox, type the URL: `https://www.bitabiz.com/dashboard`</span></span>

1. <span data-ttu-id="9a28c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9a28c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/bitabiz-tutorial/tutorial_bitabiz_certificate.png) 

1. <span data-ttu-id="9a28c-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9a28c-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bitabiz-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="9a28c-165">On the **BitaBIZ Configuration** section, click **Configure BitaBIZ** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9a28c-165">On the **BitaBIZ Configuration** section, click **Configure BitaBIZ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9a28c-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9a28c-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![BitaBIZ Configuration](./media/bitabiz-tutorial/tutorial_bitabiz_configure.png) 

1. <span data-ttu-id="9a28c-168">In a different web browser window, sign-on to your BitaBIZ tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9a28c-168">In a different web browser window, sign-on to your BitaBIZ tenant as an administrator.</span></span>

1. <span data-ttu-id="9a28c-169">Click on **SETUP ADMIN**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-169">Click on **SETUP ADMIN**.</span></span>

    ![BitaBIZ Configuration](./media/bitabiz-tutorial/settings1.png)

1. <span data-ttu-id="9a28c-171">Click on **Microsoft integrations** under **Add value** section.</span><span class="sxs-lookup"><span data-stu-id="9a28c-171">Click on **Microsoft integrations** under **Add value** section.</span></span>

    ![BitaBIZ Configuration](./media/bitabiz-tutorial/settings2.png)

1. <span data-ttu-id="9a28c-173">Scroll down to the section **Microsoft Azure AD (Enable single sign on)** and perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9a28c-173">Scroll down to the section **Microsoft Azure AD (Enable single sign on)** and perform following steps:</span></span>

    ![BitaBIZ Configuration](./media/bitabiz-tutorial/settings3.png)

    <span data-ttu-id="9a28c-175">a.</span><span class="sxs-lookup"><span data-stu-id="9a28c-175">a.</span></span> <span data-ttu-id="9a28c-176">Copy the value from the **Entity ID (”Identifier” in Azure AD)** textbox and paste it into the **Identifier** textbox on the **BitaBIZ Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a28c-176">Copy the value from the **Entity ID (”Identifier” in Azure AD)** textbox and paste it into the **Identifier** textbox on the **BitaBIZ Domain and URLs** section in Azure portal.</span></span> 
    
    <span data-ttu-id="9a28c-177">b.</span><span class="sxs-lookup"><span data-stu-id="9a28c-177">b.</span></span> <span data-ttu-id="9a28c-178">In the **Azure AD Single Sign-On Service URL** textbox, paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a28c-178">In the **Azure AD Single Sign-On Service URL** textbox, paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="9a28c-179">c.</span><span class="sxs-lookup"><span data-stu-id="9a28c-179">c.</span></span> <span data-ttu-id="9a28c-180">In the **Azure AD SAML Entity ID** textbox, paste **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a28c-180">In the **Azure AD SAML Entity ID** textbox, paste **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9a28c-181">d.</span><span class="sxs-lookup"><span data-stu-id="9a28c-181">d.</span></span> <span data-ttu-id="9a28c-182">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Azure AD Signing Certificate (Base64 encoded)** textbox.</span><span class="sxs-lookup"><span data-stu-id="9a28c-182">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Azure AD Signing Certificate (Base64 encoded)** textbox.</span></span>

    <span data-ttu-id="9a28c-183">e.</span><span class="sxs-lookup"><span data-stu-id="9a28c-183">e.</span></span> <span data-ttu-id="9a28c-184">Add your business e-mail domain name that is, mycompany.com in **Domain name** textbox to assign SSO to the users in your company with this email domain (NOT MANDATORY).</span><span class="sxs-lookup"><span data-stu-id="9a28c-184">Add your business e-mail domain name that is, mycompany.com in **Domain name** textbox to assign SSO to the users in your company with this email domain (NOT MANDATORY).</span></span>
    
    <span data-ttu-id="9a28c-185">f.</span><span class="sxs-lookup"><span data-stu-id="9a28c-185">f.</span></span> <span data-ttu-id="9a28c-186">Mark **SSO enabled** the BitaBIZ account.</span><span class="sxs-lookup"><span data-stu-id="9a28c-186">Mark **SSO enabled** the BitaBIZ account.</span></span>
    
    <span data-ttu-id="9a28c-187">g.</span><span class="sxs-lookup"><span data-stu-id="9a28c-187">g.</span></span> <span data-ttu-id="9a28c-188">Click **Save Azure AD configuration** to save and activate the SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="9a28c-188">Click **Save Azure AD configuration** to save and activate the SSO configuration.</span></span>

> [!TIP]
> <span data-ttu-id="9a28c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9a28c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a28c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9a28c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a28c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a28c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a28c-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9a28c-192">Create an Azure AD test user</span></span>

<span data-ttu-id="9a28c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a28c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9a28c-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a28c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a28c-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9a28c-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bitabiz-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9a28c-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bitabiz-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9a28c-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9a28c-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bitabiz-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9a28c-202">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a28c-202">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bitabiz-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a28c-204">a.</span><span class="sxs-lookup"><span data-stu-id="9a28c-204">a.</span></span> <span data-ttu-id="9a28c-205">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a28c-206">b.</span><span class="sxs-lookup"><span data-stu-id="9a28c-206">b.</span></span> <span data-ttu-id="9a28c-207">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a28c-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a28c-208">c.</span><span class="sxs-lookup"><span data-stu-id="9a28c-208">c.</span></span> <span data-ttu-id="9a28c-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9a28c-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9a28c-210">d.</span><span class="sxs-lookup"><span data-stu-id="9a28c-210">d.</span></span> <span data-ttu-id="9a28c-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-211">Click **Create**.</span></span>
 
### <a name="create-a-bitabiz-test-user"></a><span data-ttu-id="9a28c-212">Create a BitaBIZ test user</span><span class="sxs-lookup"><span data-stu-id="9a28c-212">Create a BitaBIZ test user</span></span>

<span data-ttu-id="9a28c-213">To enable Azure AD users to log in to BitaBIZ, they must be provisioned into BitaBIZ.</span><span class="sxs-lookup"><span data-stu-id="9a28c-213">To enable Azure AD users to log in to BitaBIZ, they must be provisioned into BitaBIZ.</span></span>  
<span data-ttu-id="9a28c-214">In the case of BitaBIZ, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="9a28c-214">In the case of BitaBIZ, provisioning is a manual task.</span></span>

<span data-ttu-id="9a28c-215">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a28c-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9a28c-216">Log in to your BitaBIZ company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9a28c-216">Log in to your BitaBIZ company site as an administrator.</span></span>

1. <span data-ttu-id="9a28c-217">Click on **SETUP ADMIN**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-217">Click on **SETUP ADMIN**.</span></span>

    ![BitaBIZ Add User](./media/bitabiz-tutorial/settings1.png)

1. <span data-ttu-id="9a28c-219">Click on **Add users** under **Organization** section.</span><span class="sxs-lookup"><span data-stu-id="9a28c-219">Click on **Add users** under **Organization** section.</span></span>

    ![BitaBIZ Add User](./media/bitabiz-tutorial/user1.png)

1. <span data-ttu-id="9a28c-221">Click **Add new employee**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-221">Click **Add new employee**.</span></span>

    ![BitaBIZ Add User](./media/bitabiz-tutorial/user2.png)

1. <span data-ttu-id="9a28c-223">On the **“Add new employee”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a28c-223">On the **“Add new employee”** dialog page, perform the following steps:</span></span>

    ![BitaBIZ Add User](./media/bitabiz-tutorial/user3.png)

    <span data-ttu-id="9a28c-225">a.</span><span class="sxs-lookup"><span data-stu-id="9a28c-225">a.</span></span> <span data-ttu-id="9a28c-226">In the **First Name** textbox, type the first name of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="9a28c-226">In the **First Name** textbox, type the first name of user like Britta.</span></span>

    <span data-ttu-id="9a28c-227">b.</span><span class="sxs-lookup"><span data-stu-id="9a28c-227">b.</span></span> <span data-ttu-id="9a28c-228">In the **Last Name** textbox, type the last name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="9a28c-228">In the **Last Name** textbox, type the last name of user like Simon.</span></span>

    <span data-ttu-id="9a28c-229">c.</span><span class="sxs-lookup"><span data-stu-id="9a28c-229">c.</span></span> <span data-ttu-id="9a28c-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9a28c-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="9a28c-231">d.</span><span class="sxs-lookup"><span data-stu-id="9a28c-231">d.</span></span> <span data-ttu-id="9a28c-232">Select a date in **Date of employment**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-232">Select a date in **Date of employment**.</span></span>

    <span data-ttu-id="9a28c-233">e.</span><span class="sxs-lookup"><span data-stu-id="9a28c-233">e.</span></span> <span data-ttu-id="9a28c-234">There are other non-mandatory user attributes which can be set up for the user.</span><span class="sxs-lookup"><span data-stu-id="9a28c-234">There are other non-mandatory user attributes which can be set up for the user.</span></span> <span data-ttu-id="9a28c-235">Please refer the [Employee Setup Doc](https://help.bitabiz.dk/manage-or-set-up-your-account/on-boarding-employees/new-employee) for more details.</span><span class="sxs-lookup"><span data-stu-id="9a28c-235">Please refer the [Employee Setup Doc](https://help.bitabiz.dk/manage-or-set-up-your-account/on-boarding-employees/new-employee) for more details.</span></span>    
    
    <span data-ttu-id="9a28c-236">f.</span><span class="sxs-lookup"><span data-stu-id="9a28c-236">f.</span></span> <span data-ttu-id="9a28c-237">Click **Save employee**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-237">Click **Save employee**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9a28c-238">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="9a28c-238">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>
    
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9a28c-239">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9a28c-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="9a28c-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BitaBIZ.</span><span class="sxs-lookup"><span data-stu-id="9a28c-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BitaBIZ.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9a28c-242">**To assign Britta Simon to BitaBIZ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9a28c-242">**To assign Britta Simon to BitaBIZ, perform the following steps:**</span></span>

1. <span data-ttu-id="9a28c-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9a28c-245">In the applications list, select **BitaBIZ**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-245">In the applications list, select **BitaBIZ**.</span></span>

    ![The BitaBIZ link in the Applications list](./media/bitabiz-tutorial/tutorial_bitabiz_app.png)  

1. <span data-ttu-id="9a28c-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9a28c-247">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9a28c-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9a28c-249">Click **Add** button.</span></span> <span data-ttu-id="9a28c-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9a28c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9a28c-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9a28c-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9a28c-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9a28c-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9a28c-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9a28c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a28c-255">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9a28c-255">Test single sign-on</span></span>

<span data-ttu-id="9a28c-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9a28c-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a28c-257">When you click the BitaBIZ tile in the Access Panel, you should get automatically signed-on to your BitaBIZ application.</span><span class="sxs-lookup"><span data-stu-id="9a28c-257">When you click the BitaBIZ tile in the Access Panel, you should get automatically signed-on to your BitaBIZ application.</span></span>
<span data-ttu-id="9a28c-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a28c-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a28c-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9a28c-259">Additional resources</span></span>

* [<span data-ttu-id="9a28c-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a28c-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9a28c-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a28c-261">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bitabiz-tutorial/tutorial_general_01.png
[2]: ./media/bitabiz-tutorial/tutorial_general_02.png
[3]: ./media/bitabiz-tutorial/tutorial_general_03.png
[4]: ./media/bitabiz-tutorial/tutorial_general_04.png

[100]: ./media/bitabiz-tutorial/tutorial_general_100.png

[200]: ./media/bitabiz-tutorial/tutorial_general_200.png
[201]: ./media/bitabiz-tutorial/tutorial_general_201.png
[202]: ./media/bitabiz-tutorial/tutorial_general_202.png
[203]: ./media/bitabiz-tutorial/tutorial_general_203.png

