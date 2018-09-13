---
title: 'Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Perception United States (Non-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 61fb9904e69f5269c345b733ef2396294c6c790a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866572"
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="4dc03-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="4dc03-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="4dc03-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dc03-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dc03-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4dc03-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4dc03-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4dc03-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="4dc03-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4dc03-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4dc03-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4dc03-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4dc03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4dc03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dc03-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4dc03-110">Prerequisites</span></span>

<span data-ttu-id="4dc03-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4dc03-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="4dc03-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4dc03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dc03-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4dc03-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dc03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4dc03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dc03-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4dc03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dc03-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4dc03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4dc03-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dc03-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dc03-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4dc03-118">Scenario description</span></span>
<span data-ttu-id="4dc03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4dc03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dc03-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dc03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dc03-121">Adding Perception United States (Non-UltiPro) from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dc03-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
1. <span data-ttu-id="4dc03-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dc03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="4dc03-123">Adding Perception United States (Non-UltiPro) from the gallery</span><span class="sxs-lookup"><span data-stu-id="4dc03-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="4dc03-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4dc03-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4dc03-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dc03-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4dc03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4dc03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="4dc03-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4dc03-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="4dc03-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4dc03-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="4dc03-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4dc03-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![Perception United States (Non-UltiPro) in the results list](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4dc03-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dc03-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4dc03-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4dc03-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4dc03-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dc03-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="4dc03-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4dc03-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="4dc03-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4dc03-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4dc03-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4dc03-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4dc03-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4dc03-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4dc03-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dc03-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4dc03-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4dc03-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4dc03-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dc03-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4dc03-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4dc03-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4dc03-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dc03-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4dc03-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span><span class="sxs-lookup"><span data-stu-id="4dc03-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="4dc03-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dc03-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="4dc03-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="4dc03-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4dc03-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

1. <span data-ttu-id="4dc03-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dc03-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Perception United States (Non-UltiPro) Domain and URLs single sign-on information](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="4dc03-155">a.</span><span class="sxs-lookup"><span data-stu-id="4dc03-155">a.</span></span> <span data-ttu-id="4dc03-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4dc03-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="4dc03-157">b.</span><span class="sxs-lookup"><span data-stu-id="4dc03-157">b.</span></span> <span data-ttu-id="4dc03-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="4dc03-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dc03-159">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="4dc03-159">The value is not real.</span></span> <span data-ttu-id="4dc03-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4dc03-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
1. <span data-ttu-id="4dc03-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4dc03-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

1. <span data-ttu-id="4dc03-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4dc03-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/perceptionunitedstates-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4dc03-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4dc03-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4dc03-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4dc03-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="4dc03-167">a.</span><span class="sxs-lookup"><span data-stu-id="4dc03-167">a.</span></span> <span data-ttu-id="4dc03-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span><span class="sxs-lookup"><span data-stu-id="4dc03-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="4dc03-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="4dc03-170">b.</span><span class="sxs-lookup"><span data-stu-id="4dc03-170">b.</span></span> <span data-ttu-id="4dc03-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span><span class="sxs-lookup"><span data-stu-id="4dc03-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="4dc03-172">c.</span><span class="sxs-lookup"><span data-stu-id="4dc03-172">c.</span></span> <span data-ttu-id="4dc03-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="4dc03-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Perception United States (Non-UltiPro) Configuration](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

1. <span data-ttu-id="4dc03-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4dc03-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

1. <span data-ttu-id="4dc03-176">In the main toolbar, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Perception United States (Non-UltiPro) user](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

1. <span data-ttu-id="4dc03-178">On the **Account Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dc03-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Perception United States (Non-UltiPro) user](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="4dc03-180">a.</span><span class="sxs-lookup"><span data-stu-id="4dc03-180">a.</span></span> <span data-ttu-id="4dc03-181">In the **Company Name** textbox, type the name of the **Company**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="4dc03-182">b.</span><span class="sxs-lookup"><span data-stu-id="4dc03-182">b.</span></span> <span data-ttu-id="4dc03-183">In the **Account Name** textbox, type the name of the **Account**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="4dc03-184">c.</span><span class="sxs-lookup"><span data-stu-id="4dc03-184">c.</span></span> <span data-ttu-id="4dc03-185">In **Default Reply-To Email** text box, type the valid **Email**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="4dc03-186">d.</span><span class="sxs-lookup"><span data-stu-id="4dc03-186">d.</span></span> <span data-ttu-id="4dc03-187">Select **SSO Identity Provider** as **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

1. <span data-ttu-id="4dc03-188">On the **SSO Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dc03-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Perception United States (Non-UltiPro) SSOConfig](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="4dc03-190">a.</span><span class="sxs-lookup"><span data-stu-id="4dc03-190">a.</span></span> <span data-ttu-id="4dc03-191">Select **SAML NameID Type** as **EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="4dc03-192">b.</span><span class="sxs-lookup"><span data-stu-id="4dc03-192">b.</span></span> <span data-ttu-id="4dc03-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="4dc03-194">c.</span><span class="sxs-lookup"><span data-stu-id="4dc03-194">c.</span></span> <span data-ttu-id="4dc03-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4dc03-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4dc03-196">d.</span><span class="sxs-lookup"><span data-stu-id="4dc03-196">d.</span></span> <span data-ttu-id="4dc03-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="4dc03-198">e.</span><span class="sxs-lookup"><span data-stu-id="4dc03-198">e.</span></span> <span data-ttu-id="4dc03-199">Click on **Upload Again** to upload the **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="4dc03-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="4dc03-200">f.</span><span class="sxs-lookup"><span data-stu-id="4dc03-200">f.</span></span> <span data-ttu-id="4dc03-201">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="4dc03-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4dc03-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4dc03-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4dc03-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4dc03-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4dc03-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4dc03-205">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dc03-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4dc03-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dc03-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="4dc03-208">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dc03-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4dc03-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4dc03-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/perceptionunitedstates-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="4dc03-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/perceptionunitedstates-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="4dc03-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4dc03-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/perceptionunitedstates-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="4dc03-215">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4dc03-215">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4dc03-217">a.</span><span class="sxs-lookup"><span data-stu-id="4dc03-217">a.</span></span> <span data-ttu-id="4dc03-218">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dc03-219">b.</span><span class="sxs-lookup"><span data-stu-id="4dc03-219">b.</span></span> <span data-ttu-id="4dc03-220">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dc03-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4dc03-221">c.</span><span class="sxs-lookup"><span data-stu-id="4dc03-221">c.</span></span> <span data-ttu-id="4dc03-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4dc03-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4dc03-223">d.</span><span class="sxs-lookup"><span data-stu-id="4dc03-223">d.</span></span> <span data-ttu-id="4dc03-224">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="4dc03-225">Create a Perception United States (Non-UltiPro) test user</span><span class="sxs-lookup"><span data-stu-id="4dc03-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="4dc03-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4dc03-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="4dc03-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span><span class="sxs-lookup"><span data-stu-id="4dc03-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4dc03-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4dc03-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="4dc03-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4dc03-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![Assign the user role][200] 

<span data-ttu-id="4dc03-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4dc03-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="4dc03-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4dc03-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![The Perception United States (Non-UltiPro) link in the Applications list](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

1. <span data-ttu-id="4dc03-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4dc03-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="4dc03-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4dc03-238">Click **Add** button.</span></span> <span data-ttu-id="4dc03-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dc03-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="4dc03-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4dc03-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4dc03-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dc03-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4dc03-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4dc03-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4dc03-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4dc03-244">Test single sign-on</span></span>

<span data-ttu-id="4dc03-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4dc03-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4dc03-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span><span class="sxs-lookup"><span data-stu-id="4dc03-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="4dc03-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4dc03-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4dc03-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4dc03-248">Additional resources</span></span>

* [<span data-ttu-id="4dc03-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dc03-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4dc03-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dc03-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/perceptionunitedstates-tutorial/tutorial_general_203.png

