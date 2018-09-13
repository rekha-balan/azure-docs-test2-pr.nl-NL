---
title: 'Tutorial: Azure Active Directory integration with Mercer BenefitsCentral (MBC) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mercer BenefitsCentral (MBC).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3788b28c-49aa-4208-9acd-630362008e89
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/21/2017
ms.author: jeedes
ms.openlocfilehash: 963aff019c849b2637819296185e138d531ddef2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869106"
---
# <a name="tutorial-azure-active-directory-integration-with-mercer-benefitscentral-mbc"></a><span data-ttu-id="09543-103">Tutorial: Azure Active Directory integration with Mercer BenefitsCentral (MBC)</span><span class="sxs-lookup"><span data-stu-id="09543-103">Tutorial: Azure Active Directory integration with Mercer BenefitsCentral (MBC)</span></span>

<span data-ttu-id="09543-104">In this tutorial, you learn how to integrate Mercer BenefitsCentral (MBC) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09543-104">In this tutorial, you learn how to integrate Mercer BenefitsCentral (MBC) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09543-105">Integrating Mercer BenefitsCentral (MBC) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="09543-105">Integrating Mercer BenefitsCentral (MBC) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="09543-106">You can control in Azure AD who has access to Mercer BenefitsCentral (MBC).</span><span class="sxs-lookup"><span data-stu-id="09543-106">You can control in Azure AD who has access to Mercer BenefitsCentral (MBC).</span></span>
- <span data-ttu-id="09543-107">You can enable your users to automatically get signed-on to Mercer BenefitsCentral (MBC) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="09543-107">You can enable your users to automatically get signed-on to Mercer BenefitsCentral (MBC) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="09543-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="09543-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="09543-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="09543-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09543-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09543-110">Prerequisites</span></span>

<span data-ttu-id="09543-111">To configure Azure AD integration with Mercer BenefitsCentral (MBC), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="09543-111">To configure Azure AD integration with Mercer BenefitsCentral (MBC), you need the following items:</span></span>

- <span data-ttu-id="09543-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="09543-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09543-113">A Mercer BenefitsCentral (MBC) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="09543-113">A Mercer BenefitsCentral (MBC) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09543-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="09543-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09543-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="09543-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09543-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="09543-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="09543-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09543-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09543-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="09543-118">Scenario description</span></span>
<span data-ttu-id="09543-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="09543-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09543-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="09543-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09543-121">Adding Mercer BenefitsCentral (MBC) from the gallery</span><span class="sxs-lookup"><span data-stu-id="09543-121">Adding Mercer BenefitsCentral (MBC) from the gallery</span></span>
1. <span data-ttu-id="09543-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="09543-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mercer-benefitscentral-mbc-from-the-gallery"></a><span data-ttu-id="09543-123">Adding Mercer BenefitsCentral (MBC) from the gallery</span><span class="sxs-lookup"><span data-stu-id="09543-123">Adding Mercer BenefitsCentral (MBC) from the gallery</span></span>
<span data-ttu-id="09543-124">To configure the integration of Mercer BenefitsCentral (MBC) into Azure AD, you need to add Mercer BenefitsCentral (MBC) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="09543-124">To configure the integration of Mercer BenefitsCentral (MBC) into Azure AD, you need to add Mercer BenefitsCentral (MBC) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09543-125">**To add Mercer BenefitsCentral (MBC) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09543-125">**To add Mercer BenefitsCentral (MBC) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09543-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="09543-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="09543-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="09543-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="09543-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="09543-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="09543-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="09543-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="09543-133">In the search box, type **Mercer BenefitsCentral (MBC)**, select **Mercer BenefitsCentral (MBC)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="09543-133">In the search box, type **Mercer BenefitsCentral (MBC)**, select **Mercer BenefitsCentral (MBC)** from result panel then click **Add** button to add the application.</span></span>

    ![Mercer BenefitsCentral (MBC) in the results list](./media/mercerhrs-tutorial/tutorial_mercerhrs_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="09543-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="09543-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="09543-136">In this section, you configure and test Azure AD single sign-on with Mercer BenefitsCentral (MBC) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="09543-136">In this section, you configure and test Azure AD single sign-on with Mercer BenefitsCentral (MBC) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09543-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mercer BenefitsCentral (MBC) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09543-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mercer BenefitsCentral (MBC) is to a user in Azure AD.</span></span> <span data-ttu-id="09543-138">In other words, a link relationship between an Azure AD user and the related user in Mercer BenefitsCentral (MBC) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="09543-138">In other words, a link relationship between an Azure AD user and the related user in Mercer BenefitsCentral (MBC) needs to be established.</span></span>

<span data-ttu-id="09543-139">In Mercer BenefitsCentral (MBC), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="09543-139">In Mercer BenefitsCentral (MBC), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="09543-140">To configure and test Azure AD single sign-on with Mercer BenefitsCentral (MBC), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="09543-140">To configure and test Azure AD single sign-on with Mercer BenefitsCentral (MBC), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09543-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="09543-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="09543-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09543-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="09543-143">**[Create a Mercer BenefitsCentral (MBC) test user](#create-a-mercer-benefitscentral-mbc-test-user)** - to have a counterpart of Britta Simon in Mercer BenefitsCentral (MBC) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="09543-143">**[Create a Mercer BenefitsCentral (MBC) test user](#create-a-mercer-benefitscentral-mbc-test-user)** - to have a counterpart of Britta Simon in Mercer BenefitsCentral (MBC) that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="09543-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="09543-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="09543-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="09543-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="09543-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="09543-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="09543-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mercer BenefitsCentral (MBC) application.</span><span class="sxs-lookup"><span data-stu-id="09543-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mercer BenefitsCentral (MBC) application.</span></span>

<span data-ttu-id="09543-148">**To configure Azure AD single sign-on with Mercer BenefitsCentral (MBC), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09543-148">**To configure Azure AD single sign-on with Mercer BenefitsCentral (MBC), perform the following steps:**</span></span>

1. <span data-ttu-id="09543-149">In the Azure portal, on the **Mercer BenefitsCentral (MBC)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="09543-149">In the Azure portal, on the **Mercer BenefitsCentral (MBC)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="09543-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="09543-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/mercerhrs-tutorial/tutorial_mercerhrs_samlbase.png)

1. <span data-ttu-id="09543-153">On the **Mercer BenefitsCentral (MBC) Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09543-153">On the **Mercer BenefitsCentral (MBC) Domain and URLs** section, perform the following steps:</span></span>

    ![Mercer BenefitsCentral (MBC) Domain and URLs single sign-on information](./media/mercerhrs-tutorial/tutorial_mercerhrs_url.png)

    <span data-ttu-id="09543-155">a.</span><span class="sxs-lookup"><span data-stu-id="09543-155">a.</span></span> <span data-ttu-id="09543-156">In the **Identifier** textbox, type a URL using the following pattern: `stg.mercerhrs.com/saml2.0`</span><span class="sxs-lookup"><span data-stu-id="09543-156">In the **Identifier** textbox, type a URL using the following pattern: `stg.mercerhrs.com/saml2.0`</span></span>

    <span data-ttu-id="09543-157">b.</span><span class="sxs-lookup"><span data-stu-id="09543-157">b.</span></span> <span data-ttu-id="09543-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://ssous-stg.mercerhrs.com/SP2/Saml2AssertionConsumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="09543-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://ssous-stg.mercerhrs.com/SP2/Saml2AssertionConsumer.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="09543-159">Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="09543-159">Reply URL value is not real.</span></span> <span data-ttu-id="09543-160">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="09543-160">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="09543-161">Contact [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html) to get this value.</span><span class="sxs-lookup"><span data-stu-id="09543-161">Contact [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html) to get this value.</span></span>

1. <span data-ttu-id="09543-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="09543-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/mercerhrs-tutorial/tutorial_mercerhrs_certificate.png) 

1. <span data-ttu-id="09543-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="09543-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mercerhrs-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="09543-166">On the **Mercer BenefitsCentral (MBC) Configuration** section, click **Configure Mercer BenefitsCentral (MBC)** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="09543-166">On the **Mercer BenefitsCentral (MBC) Configuration** section, click **Configure Mercer BenefitsCentral (MBC)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="09543-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="09543-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Mercer BenefitsCentral (MBC) Configuration](./media/mercerhrs-tutorial/tutorial_mercerhrs_configure.png) 

1. <span data-ttu-id="09543-169">To configure single sign-on on **Mercer BenefitsCentral (MBC)** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html).</span><span class="sxs-lookup"><span data-stu-id="09543-169">To configure single sign-on on **Mercer BenefitsCentral (MBC)** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html).</span></span> <span data-ttu-id="09543-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="09543-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="09543-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="09543-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="09543-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="09543-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="09543-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="09543-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="09543-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09543-174">Create an Azure AD test user</span></span>

<span data-ttu-id="09543-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09543-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="09543-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09543-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09543-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="09543-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mercerhrs-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="09543-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="09543-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mercerhrs-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="09543-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="09543-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mercerhrs-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="09543-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09543-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mercerhrs-tutorial/create_aaduser_04.png)

    <span data-ttu-id="09543-186">a.</span><span class="sxs-lookup"><span data-stu-id="09543-186">a.</span></span> <span data-ttu-id="09543-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09543-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09543-188">b.</span><span class="sxs-lookup"><span data-stu-id="09543-188">b.</span></span> <span data-ttu-id="09543-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09543-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="09543-190">c.</span><span class="sxs-lookup"><span data-stu-id="09543-190">c.</span></span> <span data-ttu-id="09543-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="09543-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="09543-192">d.</span><span class="sxs-lookup"><span data-stu-id="09543-192">d.</span></span> <span data-ttu-id="09543-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="09543-193">Click **Create**.</span></span>
  
### <a name="create-a-mercer-benefitscentral-mbc-test-user"></a><span data-ttu-id="09543-194">Create a Mercer BenefitsCentral (MBC) test user</span><span class="sxs-lookup"><span data-stu-id="09543-194">Create a Mercer BenefitsCentral (MBC) test user</span></span>

<span data-ttu-id="09543-195">In this section, you create a user called Britta Simon in Mercer HRS.</span><span class="sxs-lookup"><span data-stu-id="09543-195">In this section, you create a user called Britta Simon in Mercer HRS.</span></span> <span data-ttu-id="09543-196">Work with [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html) to add the users in the Mercer HRS platform.</span><span class="sxs-lookup"><span data-stu-id="09543-196">Work with [Mercer BenefitsCentral (MBC) support team](https://www.mercer.com/contact-us.html) to add the users in the Mercer HRS platform.</span></span> <span data-ttu-id="09543-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="09543-197">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="09543-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09543-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="09543-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mercer BenefitsCentral (MBC).</span><span class="sxs-lookup"><span data-stu-id="09543-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mercer BenefitsCentral (MBC).</span></span>

![Assign the user role][200] 

<span data-ttu-id="09543-201">**To assign Britta Simon to Mercer BenefitsCentral (MBC), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09543-201">**To assign Britta Simon to Mercer BenefitsCentral (MBC), perform the following steps:**</span></span>

1. <span data-ttu-id="09543-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="09543-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="09543-204">In the applications list, select **Mercer BenefitsCentral (MBC)**.</span><span class="sxs-lookup"><span data-stu-id="09543-204">In the applications list, select **Mercer BenefitsCentral (MBC)**.</span></span>

    ![The Mercer BenefitsCentral (MBC) link in the Applications list](./media/mercerhrs-tutorial/tutorial_mercerhrs_app.png)  

1. <span data-ttu-id="09543-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="09543-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="09543-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="09543-208">Click **Add** button.</span></span> <span data-ttu-id="09543-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="09543-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="09543-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="09543-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="09543-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="09543-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="09543-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="09543-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="09543-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="09543-214">Test single sign-on</span></span>

<span data-ttu-id="09543-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="09543-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="09543-216">When you click the Mercer BenefitsCentral (MBC) tile in the Access Panel, you should get automatically signed-on to your Mercer BenefitsCentral (MBC) application.</span><span class="sxs-lookup"><span data-stu-id="09543-216">When you click the Mercer BenefitsCentral (MBC) tile in the Access Panel, you should get automatically signed-on to your Mercer BenefitsCentral (MBC) application.</span></span>
<span data-ttu-id="09543-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="09543-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="09543-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="09543-218">Additional resources</span></span>

* [<span data-ttu-id="09543-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09543-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="09543-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09543-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mercerhrs-tutorial/tutorial_general_01.png
[2]: ./media/mercerhrs-tutorial/tutorial_general_02.png
[3]: ./media/mercerhrs-tutorial/tutorial_general_03.png
[4]: ./media/mercerhrs-tutorial/tutorial_general_04.png

[100]: ./media/mercerhrs-tutorial/tutorial_general_100.png

[200]: ./media/mercerhrs-tutorial/tutorial_general_200.png
[201]: ./media/mercerhrs-tutorial/tutorial_general_201.png
[202]: ./media/mercerhrs-tutorial/tutorial_general_202.png
[203]: ./media/mercerhrs-tutorial/tutorial_general_203.png

