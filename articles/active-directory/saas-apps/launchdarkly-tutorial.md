---
title: 'Tutorial: Azure Active Directory integration with LaunchDarkly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LaunchDarkly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0e9cb37e-16bf-493b-bfc8-8d9840545a1e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2018
ms.author: jeedes
ms.openlocfilehash: 54bf459f6acd7649f3ad1a546bef1d0429393161
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856273"
---
# <a name="tutorial-azure-active-directory-integration-with-launchdarkly"></a><span data-ttu-id="4edc8-103">Tutorial: Azure Active Directory integration with LaunchDarkly</span><span class="sxs-lookup"><span data-stu-id="4edc8-103">Tutorial: Azure Active Directory integration with LaunchDarkly</span></span>

<span data-ttu-id="4edc8-104">In this tutorial, you learn how to integrate LaunchDarkly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4edc8-104">In this tutorial, you learn how to integrate LaunchDarkly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4edc8-105">Integrating LaunchDarkly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4edc8-105">Integrating LaunchDarkly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4edc8-106">You can control in Azure AD who has access to LaunchDarkly.</span><span class="sxs-lookup"><span data-stu-id="4edc8-106">You can control in Azure AD who has access to LaunchDarkly.</span></span>
- <span data-ttu-id="4edc8-107">You can enable your users to automatically get signed-on to LaunchDarkly (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4edc8-107">You can enable your users to automatically get signed-on to LaunchDarkly (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4edc8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4edc8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4edc8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4edc8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4edc8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4edc8-110">Prerequisites</span></span>

<span data-ttu-id="4edc8-111">To configure Azure AD integration with LaunchDarkly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4edc8-111">To configure Azure AD integration with LaunchDarkly, you need the following items:</span></span>

- <span data-ttu-id="4edc8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4edc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4edc8-113">A LaunchDarkly single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4edc8-113">A LaunchDarkly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4edc8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4edc8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4edc8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4edc8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4edc8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4edc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4edc8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4edc8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4edc8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4edc8-118">Scenario description</span></span>
<span data-ttu-id="4edc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4edc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4edc8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4edc8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4edc8-121">Adding LaunchDarkly from the gallery</span><span class="sxs-lookup"><span data-stu-id="4edc8-121">Adding LaunchDarkly from the gallery</span></span>
1. <span data-ttu-id="4edc8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4edc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-launchdarkly-from-the-gallery"></a><span data-ttu-id="4edc8-123">Adding LaunchDarkly from the gallery</span><span class="sxs-lookup"><span data-stu-id="4edc8-123">Adding LaunchDarkly from the gallery</span></span>
<span data-ttu-id="4edc8-124">To configure the integration of LaunchDarkly into Azure AD, you need to add LaunchDarkly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4edc8-124">To configure the integration of LaunchDarkly into Azure AD, you need to add LaunchDarkly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4edc8-125">**To add LaunchDarkly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4edc8-125">**To add LaunchDarkly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4edc8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4edc8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="4edc8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4edc8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="4edc8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4edc8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="4edc8-133">In the search box, type **LaunchDarkly**, select **LaunchDarkly** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4edc8-133">In the search box, type **LaunchDarkly**, select **LaunchDarkly** from result panel then click **Add** button to add the application.</span></span>

    ![LaunchDarkly in the results list](./media/launchdarkly-tutorial/tutorial_launchdarkly_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4edc8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4edc8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4edc8-136">In this section, you configure and test Azure AD single sign-on with LaunchDarkly based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4edc8-136">In this section, you configure and test Azure AD single sign-on with LaunchDarkly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4edc8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LaunchDarkly is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edc8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LaunchDarkly is to a user in Azure AD.</span></span> <span data-ttu-id="4edc8-138">In other words, a link relationship between an Azure AD user and the related user in LaunchDarkly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4edc8-138">In other words, a link relationship between an Azure AD user and the related user in LaunchDarkly needs to be established.</span></span>

<span data-ttu-id="4edc8-139">To configure and test Azure AD single sign-on with LaunchDarkly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4edc8-139">To configure and test Azure AD single sign-on with LaunchDarkly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4edc8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4edc8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4edc8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4edc8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4edc8-142">**[Create a LaunchDarkly test user](#create-a-launchdarkly-test-user)** - to have a counterpart of Britta Simon in LaunchDarkly that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4edc8-142">**[Create a LaunchDarkly test user](#create-a-launchdarkly-test-user)** - to have a counterpart of Britta Simon in LaunchDarkly that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4edc8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4edc8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4edc8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4edc8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4edc8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4edc8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4edc8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LaunchDarkly application.</span><span class="sxs-lookup"><span data-stu-id="4edc8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LaunchDarkly application.</span></span>

<span data-ttu-id="4edc8-147">**To configure Azure AD single sign-on with LaunchDarkly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4edc8-147">**To configure Azure AD single sign-on with LaunchDarkly, perform the following steps:**</span></span>

1. <span data-ttu-id="4edc8-148">In the Azure portal, on the **LaunchDarkly** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-148">In the Azure portal, on the **LaunchDarkly** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="4edc8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4edc8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/launchdarkly-tutorial/tutorial_launchdarkly_samlbase.png)

1. <span data-ttu-id="4edc8-152">On the **LaunchDarkly Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4edc8-152">On the **LaunchDarkly Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![LaunchDarkly Domain and URLs single sign-on information](./media/launchdarkly-tutorial/tutorial_launchdarkly_url.png)

    <span data-ttu-id="4edc8-154">a.</span><span class="sxs-lookup"><span data-stu-id="4edc8-154">a.</span></span> <span data-ttu-id="4edc8-155">In the **Identifier (Entity ID)** textbox, type the URL: `app.launchdarkly.com`</span><span class="sxs-lookup"><span data-stu-id="4edc8-155">In the **Identifier (Entity ID)** textbox, type the URL: `app.launchdarkly.com`</span></span>

    <span data-ttu-id="4edc8-156">b.</span><span class="sxs-lookup"><span data-stu-id="4edc8-156">b.</span></span> <span data-ttu-id="4edc8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.launchdarkly.com/trust/saml2/acs/<customers-unique-id>`</span><span class="sxs-lookup"><span data-stu-id="4edc8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.launchdarkly.com/trust/saml2/acs/<customers-unique-id>`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4edc8-158">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="4edc8-158">The Reply URL value is not real.</span></span> <span data-ttu-id="4edc8-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4edc8-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="4edc8-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4edc8-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![LaunchDarkly Domain and URLs single sign-on information](./media/launchdarkly-tutorial/tutorial_launchdarkly_url1.png)

    <span data-ttu-id="4edc8-162">In the **Sign-on URL** textbox, type the URL: `https://app.launchdarkly.com`</span><span class="sxs-lookup"><span data-stu-id="4edc8-162">In the **Sign-on URL** textbox, type the URL: `https://app.launchdarkly.com`</span></span>

1. <span data-ttu-id="4edc8-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4edc8-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/launchdarkly-tutorial/tutorial_launchdarkly_certificate.png) 

1. <span data-ttu-id="4edc8-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4edc8-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/launchdarkly-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="4edc8-167">On the **LaunchDarkly Configuration** section, click **Configure LaunchDarkly** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4edc8-167">On the **LaunchDarkly Configuration** section, click **Configure LaunchDarkly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4edc8-168">Copy the **Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4edc8-168">Copy the **Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![LaunchDarkly Configuration](./media/launchdarkly-tutorial/tutorial_launchdarkly_configure.png)

1. <span data-ttu-id="4edc8-170">In a different web browser window, log into your LaunchDarkly company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4edc8-170">In a different web browser window, log into your LaunchDarkly company site as an administrator.</span></span>

1. <span data-ttu-id="4edc8-171">Select **Account Settings** from the left navigation panel.</span><span class="sxs-lookup"><span data-stu-id="4edc8-171">Select **Account Settings** from the left navigation panel.</span></span>

    ![LaunchDarkly Configuration](./media/launchdarkly-tutorial/configure1.png)

1. <span data-ttu-id="4edc8-173">Click **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="4edc8-173">Click **Security** tab.</span></span>

    ![LaunchDarkly Configuration](./media/launchdarkly-tutorial/configure2.png)

1. <span data-ttu-id="4edc8-175">Click **ENABLE SSO** and then **EDIT SAML CONFIGURATION**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-175">Click **ENABLE SSO** and then **EDIT SAML CONFIGURATION**.</span></span>

    ![LaunchDarkly Configuration](./media/launchdarkly-tutorial/configure3.png)

1. <span data-ttu-id="4edc8-177">On the **Edit your SAML configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4edc8-177">On the **Edit your SAML configuration** section, perform the following steps:</span></span>

    ![LaunchDarkly Configuration](./media/launchdarkly-tutorial/configure4.png)

    <span data-ttu-id="4edc8-179">a.</span><span class="sxs-lookup"><span data-stu-id="4edc8-179">a.</span></span> <span data-ttu-id="4edc8-180">Copy the **SAML consumer service URL** for your instance and paste it in Reply URL textbox in **LaunchDarkly Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4edc8-180">Copy the **SAML consumer service URL** for your instance and paste it in Reply URL textbox in **LaunchDarkly Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="4edc8-181">b.</span><span class="sxs-lookup"><span data-stu-id="4edc8-181">b.</span></span> <span data-ttu-id="4edc8-182">In the **Sign-on URL** textbox, paste the **Single Sign-On Service URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4edc8-182">In the **Sign-on URL** textbox, paste the **Single Sign-On Service URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="4edc8-183">c.</span><span class="sxs-lookup"><span data-stu-id="4edc8-183">c.</span></span> <span data-ttu-id="4edc8-184">Open the downloaded certificate from the Azure portal into Notepad, copy the content and then paste it into the **X.509 certificate** box or you can directly upload the certificate by clicking the **upload one**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-184">Open the downloaded certificate from the Azure portal into Notepad, copy the content and then paste it into the **X.509 certificate** box or you can directly upload the certificate by clicking the **upload one**.</span></span>

    <span data-ttu-id="4edc8-185">d.</span><span class="sxs-lookup"><span data-stu-id="4edc8-185">d.</span></span> <span data-ttu-id="4edc8-186">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="4edc8-186">Click **Save**</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4edc8-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4edc8-187">Create an Azure AD test user</span></span>

<span data-ttu-id="4edc8-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4edc8-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="4edc8-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4edc8-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4edc8-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4edc8-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/launchdarkly-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="4edc8-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/launchdarkly-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="4edc8-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4edc8-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/launchdarkly-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="4edc8-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4edc8-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/launchdarkly-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4edc8-199">a.</span><span class="sxs-lookup"><span data-stu-id="4edc8-199">a.</span></span> <span data-ttu-id="4edc8-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4edc8-201">b.</span><span class="sxs-lookup"><span data-stu-id="4edc8-201">b.</span></span> <span data-ttu-id="4edc8-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4edc8-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4edc8-203">c.</span><span class="sxs-lookup"><span data-stu-id="4edc8-203">c.</span></span> <span data-ttu-id="4edc8-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4edc8-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4edc8-205">d.</span><span class="sxs-lookup"><span data-stu-id="4edc8-205">d.</span></span> <span data-ttu-id="4edc8-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-206">Click **Create**.</span></span>

### <a name="create-a-launchdarkly-test-user"></a><span data-ttu-id="4edc8-207">Create a LaunchDarkly test user</span><span class="sxs-lookup"><span data-stu-id="4edc8-207">Create a LaunchDarkly test user</span></span>

<span data-ttu-id="4edc8-208">The objective of this section is to create a user called Britta Simon in LaunchDarkly.</span><span class="sxs-lookup"><span data-stu-id="4edc8-208">The objective of this section is to create a user called Britta Simon in LaunchDarkly.</span></span> <span data-ttu-id="4edc8-209">LaunchDarkly supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="4edc8-209">LaunchDarkly supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4edc8-210">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="4edc8-210">There is no action item for you in this section.</span></span> <span data-ttu-id="4edc8-211">A new user is created during an attempt to access LaunchDarkly if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="4edc8-211">A new user is created during an attempt to access LaunchDarkly if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="4edc8-212">If you need to create a user manually, contact [LaunchDarkly Client support team](mailto:support@launchdarkly.com).</span><span class="sxs-lookup"><span data-stu-id="4edc8-212">If you need to create a user manually, contact [LaunchDarkly Client support team](mailto:support@launchdarkly.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4edc8-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4edc8-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="4edc8-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LaunchDarkly.</span><span class="sxs-lookup"><span data-stu-id="4edc8-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LaunchDarkly.</span></span>

![Assign the user role][200] 

<span data-ttu-id="4edc8-216">**To assign Britta Simon to LaunchDarkly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4edc8-216">**To assign Britta Simon to LaunchDarkly, perform the following steps:**</span></span>

1. <span data-ttu-id="4edc8-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4edc8-219">In the applications list, select **LaunchDarkly**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-219">In the applications list, select **LaunchDarkly**.</span></span>

    ![The LaunchDarkly link in the Applications list](./media/launchdarkly-tutorial/tutorial_launchdarkly_app.png)  

1. <span data-ttu-id="4edc8-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4edc8-221">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="4edc8-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4edc8-223">Click **Add** button.</span></span> <span data-ttu-id="4edc8-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4edc8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="4edc8-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4edc8-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4edc8-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4edc8-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4edc8-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4edc8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="4edc8-229">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4edc8-229">Test single sign-on</span></span>

<span data-ttu-id="4edc8-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4edc8-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4edc8-231">When you click the LaunchDarkly tile in the Access Panel, you should get automatically signed-on to your LaunchDarkly application.</span><span class="sxs-lookup"><span data-stu-id="4edc8-231">When you click the LaunchDarkly tile in the Access Panel, you should get automatically signed-on to your LaunchDarkly application.</span></span>
<span data-ttu-id="4edc8-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4edc8-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4edc8-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4edc8-233">Additional resources</span></span>

* [<span data-ttu-id="4edc8-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edc8-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4edc8-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4edc8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/launchdarkly-tutorial/tutorial_general_01.png
[2]: ./media/launchdarkly-tutorial/tutorial_general_02.png
[3]: ./media/launchdarkly-tutorial/tutorial_general_03.png
[4]: ./media/launchdarkly-tutorial/tutorial_general_04.png

[100]: ./media/launchdarkly-tutorial/tutorial_general_100.png

[200]: ./media/launchdarkly-tutorial/tutorial_general_200.png
[201]: ./media/launchdarkly-tutorial/tutorial_general_201.png
[202]: ./media/launchdarkly-tutorial/tutorial_general_202.png
[203]: ./media/launchdarkly-tutorial/tutorial_general_203.png

