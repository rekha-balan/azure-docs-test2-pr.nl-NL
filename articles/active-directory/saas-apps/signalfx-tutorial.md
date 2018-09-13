---
title: 'Tutorial: Azure Active Directory integration with SignalFx | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SignalFx.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6d5ab4b0-29bc-4b20-8536-d64db7530f32
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 0d21a409669cc7d7fceeec9787efbe31d880597c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865733"
---
# <a name="tutorial-azure-active-directory-integration-with-signalfx"></a><span data-ttu-id="e38e0-103">Tutorial: Azure Active Directory integration with SignalFx</span><span class="sxs-lookup"><span data-stu-id="e38e0-103">Tutorial: Azure Active Directory integration with SignalFx</span></span>

<span data-ttu-id="e38e0-104">In this tutorial, you learn how to integrate SignalFx with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e38e0-104">In this tutorial, you learn how to integrate SignalFx with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e38e0-105">Integrating SignalFx with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e38e0-105">Integrating SignalFx with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e38e0-106">You can control in Azure AD who has access to SignalFx.</span><span class="sxs-lookup"><span data-stu-id="e38e0-106">You can control in Azure AD who has access to SignalFx.</span></span>
- <span data-ttu-id="e38e0-107">You can enable your users to automatically get signed-on to SignalFx (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e38e0-107">You can enable your users to automatically get signed-on to SignalFx (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e38e0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e38e0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e38e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e38e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e38e0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e38e0-110">Prerequisites</span></span>

<span data-ttu-id="e38e0-111">To configure Azure AD integration with SignalFx, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e38e0-111">To configure Azure AD integration with SignalFx, you need the following items:</span></span>

- <span data-ttu-id="e38e0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e38e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e38e0-113">A SignalFx single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e38e0-113">A SignalFx single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e38e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e38e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e38e0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e38e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e38e0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e38e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e38e0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e38e0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e38e0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e38e0-118">Scenario description</span></span>
<span data-ttu-id="e38e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e38e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e38e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e38e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e38e0-121">Adding SignalFx from the gallery</span><span class="sxs-lookup"><span data-stu-id="e38e0-121">Adding SignalFx from the gallery</span></span>
1. <span data-ttu-id="e38e0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e38e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-signalfx-from-the-gallery"></a><span data-ttu-id="e38e0-123">Adding SignalFx from the gallery</span><span class="sxs-lookup"><span data-stu-id="e38e0-123">Adding SignalFx from the gallery</span></span>
<span data-ttu-id="e38e0-124">To configure the integration of SignalFx into Azure AD, you need to add SignalFx from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e38e0-124">To configure the integration of SignalFx into Azure AD, you need to add SignalFx from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e38e0-125">**To add SignalFx from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e38e0-125">**To add SignalFx from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e38e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e38e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e38e0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e38e0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e38e0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e38e0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e38e0-133">In the search box, type **SignalFx**, select **SignalFx** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e38e0-133">In the search box, type **SignalFx**, select **SignalFx** from result panel then click **Add** button to add the application.</span></span>

    ![SignalFx in the results list](./media/signalfx-tutorial/tutorial_signalfx_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e38e0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e38e0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e38e0-136">In this section, you configure and test Azure AD single sign-on with SignalFx based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e38e0-136">In this section, you configure and test Azure AD single sign-on with SignalFx based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e38e0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SignalFx is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e38e0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SignalFx is to a user in Azure AD.</span></span> <span data-ttu-id="e38e0-138">In other words, a link relationship between an Azure AD user and the related user in SignalFx needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e38e0-138">In other words, a link relationship between an Azure AD user and the related user in SignalFx needs to be established.</span></span>

<span data-ttu-id="e38e0-139">To configure and test Azure AD single sign-on with SignalFx, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e38e0-139">To configure and test Azure AD single sign-on with SignalFx, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e38e0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e38e0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e38e0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e38e0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e38e0-142">**[Create a SignalFx test user](#create-a-signalfx-test-user)** - to have a counterpart of Britta Simon in SignalFx that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e38e0-142">**[Create a SignalFx test user](#create-a-signalfx-test-user)** - to have a counterpart of Britta Simon in SignalFx that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e38e0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e38e0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e38e0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e38e0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e38e0-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e38e0-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e38e0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SignalFx application.</span><span class="sxs-lookup"><span data-stu-id="e38e0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SignalFx application.</span></span>

<span data-ttu-id="e38e0-147">**To configure Azure AD single sign-on with SignalFx, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e38e0-147">**To configure Azure AD single sign-on with SignalFx, perform the following steps:**</span></span>

1. <span data-ttu-id="e38e0-148">In the Azure portal, on the **SignalFx** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-148">In the Azure portal, on the **SignalFx** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e38e0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e38e0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/signalfx-tutorial/tutorial_signalfx_samlbase.png)

1. <span data-ttu-id="e38e0-152">On the **SignalFx Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e38e0-152">On the **SignalFx Domain and URLs** section, perform the following steps:</span></span>

    ![SignalFx Domain and URLs single sign-on information](./media/signalfx-tutorial/tutorial_signalfx_url.png)

    <span data-ttu-id="e38e0-154">a.</span><span class="sxs-lookup"><span data-stu-id="e38e0-154">a.</span></span> <span data-ttu-id="e38e0-155">In the **Identifier** textbox, type a URL: `https://api.signalfx.com/v1/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="e38e0-155">In the **Identifier** textbox, type a URL: `https://api.signalfx.com/v1/saml/metadata`</span></span>

    <span data-ttu-id="e38e0-156">b.</span><span class="sxs-lookup"><span data-stu-id="e38e0-156">b.</span></span> <span data-ttu-id="e38e0-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.signalfx.com/v1/saml/acs/<integration ID>`</span><span class="sxs-lookup"><span data-stu-id="e38e0-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.signalfx.com/v1/saml/acs/<integration ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e38e0-158">The preceding value is not real value.</span><span class="sxs-lookup"><span data-stu-id="e38e0-158">The preceding value is not real value.</span></span> <span data-ttu-id="e38e0-159">You update the value with the actual Reply URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="e38e0-159">You update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="e38e0-160">SignalFx application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="e38e0-160">SignalFx application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e38e0-161">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="e38e0-161">Configure the following claims for this application.</span></span> <span data-ttu-id="e38e0-162">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="e38e0-162">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="e38e0-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="e38e0-163">The following screenshot shows an example for this.</span></span>   

    ![Configure Single Sign-On](./media/signalfx-tutorial/tutorial_signalfx_attribute.png)

1. <span data-ttu-id="e38e0-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e38e0-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="e38e0-166">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="e38e0-166">Attribute Name</span></span> | <span data-ttu-id="e38e0-167">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="e38e0-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="e38e0-168">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="e38e0-168">User.FirstName</span></span>          | <span data-ttu-id="e38e0-169">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e38e0-169">user.givenname</span></span> |
    | <span data-ttu-id="e38e0-170">User.email</span><span class="sxs-lookup"><span data-stu-id="e38e0-170">User.email</span></span>          | <span data-ttu-id="e38e0-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="e38e0-171">user.mail</span></span> |
    | <span data-ttu-id="e38e0-172">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="e38e0-172">PersonImmutableID</span></span>       | <span data-ttu-id="e38e0-173">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="e38e0-173">user.userprincipalname</span></span>    |
    | <span data-ttu-id="e38e0-174">User.LastName</span><span class="sxs-lookup"><span data-stu-id="e38e0-174">User.LastName</span></span>       | <span data-ttu-id="e38e0-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="e38e0-175">user.surname</span></span>    |

    <span data-ttu-id="e38e0-176">a.</span><span class="sxs-lookup"><span data-stu-id="e38e0-176">a.</span></span> <span data-ttu-id="e38e0-177">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="e38e0-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/signalfx-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On Addattb](./media/signalfx-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e38e0-180">b.</span><span class="sxs-lookup"><span data-stu-id="e38e0-180">b.</span></span> <span data-ttu-id="e38e0-181">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="e38e0-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="e38e0-182">c.</span><span class="sxs-lookup"><span data-stu-id="e38e0-182">c.</span></span> <span data-ttu-id="e38e0-183">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="e38e0-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="e38e0-184">d.</span><span class="sxs-lookup"><span data-stu-id="e38e0-184">d.</span></span> <span data-ttu-id="e38e0-185">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="e38e0-185">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="e38e0-186">e.</span><span class="sxs-lookup"><span data-stu-id="e38e0-186">e.</span></span> <span data-ttu-id="e38e0-187">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-187">Click **Ok**.</span></span>
 
1. <span data-ttu-id="e38e0-188">On the **SAML Signing Certificate** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e38e0-188">On the **SAML Signing Certificate** section, perform the following steps:</span></span> 

    ![The Certificate download link](./media/signalfx-tutorial/tutorial_signalfx_certificate.png)

    <span data-ttu-id="e38e0-190">a.</span><span class="sxs-lookup"><span data-stu-id="e38e0-190">a.</span></span> <span data-ttu-id="e38e0-191">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="e38e0-191">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    <span data-ttu-id="e38e0-192">b.</span><span class="sxs-lookup"><span data-stu-id="e38e0-192">b.</span></span> <span data-ttu-id="e38e0-193">Click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e38e0-193">Click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

1. <span data-ttu-id="e38e0-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e38e0-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/signalfx-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e38e0-196">On the **SignalFx Configuration** section, click **Configure SignalFx** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e38e0-196">On the **SignalFx Configuration** section, click **Configure SignalFx** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e38e0-197">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e38e0-197">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![SignalFx Configuration](./media/signalfx-tutorial/tutorial_signalfx_configure.png) 

1. <span data-ttu-id="e38e0-199">Sign-on to your SignalFx company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="e38e0-199">Sign-on to your SignalFx company site as administrator.</span></span>

1. <span data-ttu-id="e38e0-200">In SignalFx, on the top click **Integrations** to open the Integrations page.</span><span class="sxs-lookup"><span data-stu-id="e38e0-200">In SignalFx, on the top click **Integrations** to open the Integrations page.</span></span>

    ![SignalFx Integration](./media/signalfx-tutorial/tutorial_signalfx_intg.png)

1. <span data-ttu-id="e38e0-202">Click on **Azure Active Directory** tile under **Login Services** section.</span><span class="sxs-lookup"><span data-stu-id="e38e0-202">Click on **Azure Active Directory** tile under **Login Services** section.</span></span>
 
    ![SignalFx saml](./media/signalfx-tutorial/tutorial_signalfx_saml.png)

1. <span data-ttu-id="e38e0-204">Click on **NEW INTEGRATION** and under the **INSTALL** tab perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e38e0-204">Click on **NEW INTEGRATION** and under the **INSTALL** tab perform the following steps:</span></span>
 
    ![SignalFx samlintgpage](./media/signalfx-tutorial/tutorial_signalfx_azure.png)

    <span data-ttu-id="e38e0-206">a.</span><span class="sxs-lookup"><span data-stu-id="e38e0-206">a.</span></span> <span data-ttu-id="e38e0-207">In the **Name** textbox type, a new integration name, like **OurOrgName SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-207">In the **Name** textbox type, a new integration name, like **OurOrgName SAML SSO**.</span></span>

    <span data-ttu-id="e38e0-208">b.</span><span class="sxs-lookup"><span data-stu-id="e38e0-208">b.</span></span> <span data-ttu-id="e38e0-209">Copy the **Integration ID** value and append with the **Reply URL** like `https://api.signalfx.com/v1/saml/acs/<integration ID>` in the **Reply URL** textbox of **SignalFx Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e38e0-209">Copy the **Integration ID** value and append with the **Reply URL** like `https://api.signalfx.com/v1/saml/acs/<integration ID>` in the **Reply URL** textbox of **SignalFx Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="e38e0-210">c.</span><span class="sxs-lookup"><span data-stu-id="e38e0-210">c.</span></span> <span data-ttu-id="e38e0-211">Click on **Upload File** to upload the **Base64 encoded certificate** downloaded from Azure portal in the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="e38e0-211">Click on **Upload File** to upload the **Base64 encoded certificate** downloaded from Azure portal in the **Certificate** textbox.</span></span>

    <span data-ttu-id="e38e0-212">d.</span><span class="sxs-lookup"><span data-stu-id="e38e0-212">d.</span></span> <span data-ttu-id="e38e0-213">In the **Issuer URL** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e38e0-213">In the **Issuer URL** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="e38e0-214">e.</span><span class="sxs-lookup"><span data-stu-id="e38e0-214">e.</span></span> <span data-ttu-id="e38e0-215">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e38e0-215">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="e38e0-216">f.</span><span class="sxs-lookup"><span data-stu-id="e38e0-216">f.</span></span> <span data-ttu-id="e38e0-217">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-217">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e38e0-218">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e38e0-218">Create an Azure AD test user</span></span>

<span data-ttu-id="e38e0-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e38e0-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e38e0-221">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e38e0-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e38e0-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e38e0-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/signalfx-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e38e0-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/signalfx-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e38e0-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e38e0-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/signalfx-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e38e0-228">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e38e0-228">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/signalfx-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e38e0-230">a.</span><span class="sxs-lookup"><span data-stu-id="e38e0-230">a.</span></span> <span data-ttu-id="e38e0-231">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e38e0-232">b.</span><span class="sxs-lookup"><span data-stu-id="e38e0-232">b.</span></span> <span data-ttu-id="e38e0-233">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e38e0-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e38e0-234">c.</span><span class="sxs-lookup"><span data-stu-id="e38e0-234">c.</span></span> <span data-ttu-id="e38e0-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e38e0-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e38e0-236">d.</span><span class="sxs-lookup"><span data-stu-id="e38e0-236">d.</span></span> <span data-ttu-id="e38e0-237">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-237">Click **Create**.</span></span>
  
### <a name="create-a-signalfx-test-user"></a><span data-ttu-id="e38e0-238">Create a SignalFx test user</span><span class="sxs-lookup"><span data-stu-id="e38e0-238">Create a SignalFx test user</span></span>

<span data-ttu-id="e38e0-239">The objective of this section is to create a user called Britta Simon in SignalFx.</span><span class="sxs-lookup"><span data-stu-id="e38e0-239">The objective of this section is to create a user called Britta Simon in SignalFx.</span></span> <span data-ttu-id="e38e0-240">SignalFx supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e38e0-240">SignalFx supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e38e0-241">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e38e0-241">There is no action item for you in this section.</span></span> <span data-ttu-id="e38e0-242">A new user is created during an attempt to access SignalFx if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e38e0-242">A new user is created during an attempt to access SignalFx if it doesn't exist yet.</span></span>

<span data-ttu-id="e38e0-243">When a user signs in to SignalFx from the SAML SSO for the first time, [SignalFx support team](mailto:kmazzola@signalfx.com) sends them an email containing a link that they must click through to authenticate.</span><span class="sxs-lookup"><span data-stu-id="e38e0-243">When a user signs in to SignalFx from the SAML SSO for the first time, [SignalFx support team](mailto:kmazzola@signalfx.com) sends them an email containing a link that they must click through to authenticate.</span></span> <span data-ttu-id="e38e0-244">This will only happen the first time the user signs in; subsequent login attempts will not require email validation.</span><span class="sxs-lookup"><span data-stu-id="e38e0-244">This will only happen the first time the user signs in; subsequent login attempts will not require email validation.</span></span>

>[!Note]
><span data-ttu-id="e38e0-245">If you need to create a user manually, contact [SignalFx support team](mailto:kmazzola@signalfx.com)</span><span class="sxs-lookup"><span data-stu-id="e38e0-245">If you need to create a user manually, contact [SignalFx support team](mailto:kmazzola@signalfx.com)</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e38e0-246">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e38e0-246">Assign the Azure AD test user</span></span>

<span data-ttu-id="e38e0-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SignalFx.</span><span class="sxs-lookup"><span data-stu-id="e38e0-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SignalFx.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e38e0-249">**To assign Britta Simon to SignalFx, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e38e0-249">**To assign Britta Simon to SignalFx, perform the following steps:**</span></span>

1. <span data-ttu-id="e38e0-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e38e0-252">In the applications list, select **SignalFx**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-252">In the applications list, select **SignalFx**.</span></span>

    ![The SignalFx link in the Applications list](./media/signalfx-tutorial/tutorial_signalfx_app.png)  

1. <span data-ttu-id="e38e0-254">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e38e0-254">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e38e0-256">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e38e0-256">Click **Add** button.</span></span> <span data-ttu-id="e38e0-257">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e38e0-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e38e0-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e38e0-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e38e0-260">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e38e0-260">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e38e0-261">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e38e0-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e38e0-262">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e38e0-262">Test single sign-on</span></span>

<span data-ttu-id="e38e0-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e38e0-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e38e0-264">When you click the SignalFx tile in the Access Panel, you should get automatically signed-on to your SignalFx application.</span><span class="sxs-lookup"><span data-stu-id="e38e0-264">When you click the SignalFx tile in the Access Panel, you should get automatically signed-on to your SignalFx application.</span></span>
<span data-ttu-id="e38e0-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e38e0-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e38e0-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e38e0-266">Additional resources</span></span>

* [<span data-ttu-id="e38e0-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e38e0-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e38e0-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e38e0-268">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/signalfx-tutorial/tutorial_general_01.png
[2]: ./media/signalfx-tutorial/tutorial_general_02.png
[3]: ./media/signalfx-tutorial/tutorial_general_03.png
[4]: ./media/signalfx-tutorial/tutorial_general_04.png

[100]: ./media/signalfx-tutorial/tutorial_general_100.png

[200]: ./media/signalfx-tutorial/tutorial_general_200.png
[201]: ./media/signalfx-tutorial/tutorial_general_201.png
[202]: ./media/signalfx-tutorial/tutorial_general_202.png
[203]: ./media/signalfx-tutorial/tutorial_general_203.png

