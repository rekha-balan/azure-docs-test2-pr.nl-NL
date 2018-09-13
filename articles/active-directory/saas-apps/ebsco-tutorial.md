---
title: 'Tutorial: Azure Active Directory integration with EBSCO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EBSCO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 144f7f65-69e9-4016-a151-fe1104fd6ba8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: jeedes
ms.openlocfilehash: 5ecb0e87d45cc01b65c91ee4c5c9d29806999269
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868698"
---
# <a name="tutorial-azure-active-directory-integration-with-ebsco"></a><span data-ttu-id="a82bd-103">Tutorial: Azure Active Directory integration with EBSCO</span><span class="sxs-lookup"><span data-stu-id="a82bd-103">Tutorial: Azure Active Directory integration with EBSCO</span></span>

<span data-ttu-id="a82bd-104">In this tutorial, you learn how to integrate EBSCO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a82bd-104">In this tutorial, you learn how to integrate EBSCO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a82bd-105">Integrating EBSCO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a82bd-105">Integrating EBSCO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a82bd-106">You can control in Azure AD who has access to EBSCO.</span><span class="sxs-lookup"><span data-stu-id="a82bd-106">You can control in Azure AD who has access to EBSCO.</span></span>
- <span data-ttu-id="a82bd-107">You can enable your users to automatically get signed-on to EBSCO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a82bd-107">You can enable your users to automatically get signed-on to EBSCO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a82bd-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a82bd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a82bd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a82bd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a82bd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a82bd-110">Prerequisites</span></span>

<span data-ttu-id="a82bd-111">To configure Azure AD integration with EBSCO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a82bd-111">To configure Azure AD integration with EBSCO, you need the following items:</span></span>

- <span data-ttu-id="a82bd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a82bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a82bd-113">An EBSCO single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a82bd-113">An EBSCO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a82bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a82bd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a82bd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a82bd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a82bd-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a82bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a82bd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a82bd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a82bd-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a82bd-118">Scenario description</span></span>
<span data-ttu-id="a82bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a82bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a82bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a82bd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a82bd-121">Adding EBSCO from the gallery</span><span class="sxs-lookup"><span data-stu-id="a82bd-121">Adding EBSCO from the gallery</span></span>
1. <span data-ttu-id="a82bd-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a82bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ebsco-from-the-gallery"></a><span data-ttu-id="a82bd-123">Adding EBSCO from the gallery</span><span class="sxs-lookup"><span data-stu-id="a82bd-123">Adding EBSCO from the gallery</span></span>
<span data-ttu-id="a82bd-124">To configure the integration of EBSCO into Azure AD, you need to add EBSCO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a82bd-124">To configure the integration of EBSCO into Azure AD, you need to add EBSCO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a82bd-125">**To add EBSCO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-125">**To add EBSCO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a82bd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a82bd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a82bd-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a82bd-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a82bd-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a82bd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a82bd-133">In the search box, type **EBSCO**, select **EBSCO** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-133">In the search box, type **EBSCO**, select **EBSCO** from result panel then click **Add** button to add the application.</span></span>

    ![EBSCO in the results list](./media/ebsco-tutorial/tutorial_ebsco_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a82bd-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a82bd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a82bd-136">In this section, you configure and test Azure AD single sign-on with EBSCO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a82bd-136">In this section, you configure and test Azure AD single sign-on with EBSCO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a82bd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EBSCO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a82bd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EBSCO is to a user in Azure AD.</span></span> <span data-ttu-id="a82bd-138">In other words, a link relationship between an Azure AD user and the related user in EBSCO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a82bd-138">In other words, a link relationship between an Azure AD user and the related user in EBSCO needs to be established.</span></span>

<span data-ttu-id="a82bd-139">To configure and test Azure AD single sign-on with EBSCO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a82bd-139">To configure and test Azure AD single sign-on with EBSCO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a82bd-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a82bd-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a82bd-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a82bd-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a82bd-142">**[Create an EBSCO test user](#create-an-ebsco-test-user)** - you can automate EBSCOhost user provisioning/personalization.</span><span class="sxs-lookup"><span data-stu-id="a82bd-142">**[Create an EBSCO test user](#create-an-ebsco-test-user)** - you can automate EBSCOhost user provisioning/personalization.</span></span> <span data-ttu-id="a82bd-143">EBSCO supports Just-In-Time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="a82bd-143">EBSCO supports Just-In-Time user provisioning.</span></span>
1. <span data-ttu-id="a82bd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a82bd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a82bd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a82bd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a82bd-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a82bd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a82bd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EBSCO application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EBSCO application.</span></span>

<span data-ttu-id="a82bd-148">**To configure Azure AD single sign-on with EBSCO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-148">**To configure Azure AD single sign-on with EBSCO, perform the following steps:**</span></span>

1. <span data-ttu-id="a82bd-149">In the Azure portal, on the **EBSCO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-149">In the Azure portal, on the **EBSCO** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a82bd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a82bd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/ebsco-tutorial/tutorial_ebsco_samlbase.png)

1. <span data-ttu-id="a82bd-153">On the **EBSCO Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a82bd-153">On the **EBSCO Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![EBSCO Domain and URLs single sign-on information](./media/ebsco-tutorial/tutorial_ebsco_url.png)

    <span data-ttu-id="a82bd-155">In the **Identifier** textbox, type a URL: `pingsso.ebscohost.com`</span><span class="sxs-lookup"><span data-stu-id="a82bd-155">In the **Identifier** textbox, type a URL: `pingsso.ebscohost.com`</span></span>

1. <span data-ttu-id="a82bd-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a82bd-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![EBSCO Domain and URLs single sign-on information](./media/ebsco-tutorial/tutorial_ebsco_url1.png)

    <span data-ttu-id="a82bd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://search.ebscohost.com/login.aspx?authtype=sso&custid=<unique EBSCO customer ID>&profile=<profile ID>`</span><span class="sxs-lookup"><span data-stu-id="a82bd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://search.ebscohost.com/login.aspx?authtype=sso&custid=<unique EBSCO customer ID>&profile=<profile ID>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a82bd-159">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="a82bd-159">The Sign-on URL value is not real.</span></span> <span data-ttu-id="a82bd-160">Update the value with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="a82bd-160">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="a82bd-161">Contact [EBSCO Client support team](mailto:sso@ebsco.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="a82bd-161">Contact [EBSCO Client support team](mailto:sso@ebsco.com) to get the value.</span></span> 

    <span data-ttu-id="a82bd-162">o   **Unique elements:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-162">o   **Unique elements:**</span></span>  

    <span data-ttu-id="a82bd-163">o   **Custid** = Enter unique EBSCO customer ID</span><span class="sxs-lookup"><span data-stu-id="a82bd-163">o   **Custid** = Enter unique EBSCO customer ID</span></span> 

    <span data-ttu-id="a82bd-164">o   **Profile** = Clients can tailor the link to direct users to a specific profile (depending on what they purchase from EBSCO).</span><span class="sxs-lookup"><span data-stu-id="a82bd-164">o   **Profile** = Clients can tailor the link to direct users to a specific profile (depending on what they purchase from EBSCO).</span></span> <span data-ttu-id="a82bd-165">They can enter a specific profile ID.</span><span class="sxs-lookup"><span data-stu-id="a82bd-165">They can enter a specific profile ID.</span></span> <span data-ttu-id="a82bd-166">The main IDs are eds (EBSCO Discovery Service) and ehost (EBSOCOhost databases).</span><span class="sxs-lookup"><span data-stu-id="a82bd-166">The main IDs are eds (EBSCO Discovery Service) and ehost (EBSOCOhost databases).</span></span> <span data-ttu-id="a82bd-167">Instructions for the same are given [here](https://help.ebsco.com/interfaces/EBSCOhost/EBSCOhost_FAQs/How_do_I_set_up_direct_links_to_EBSCOhost_profiles_and_or_databases#profile).</span><span class="sxs-lookup"><span data-stu-id="a82bd-167">Instructions for the same are given [here](https://help.ebsco.com/interfaces/EBSCOhost/EBSCOhost_FAQs/How_do_I_set_up_direct_links_to_EBSCOhost_profiles_and_or_databases#profile).</span></span>

1. <span data-ttu-id="a82bd-168">EBSCO application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="a82bd-168">EBSCO application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a82bd-169">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-169">Configure the following claims for this application.</span></span> <span data-ttu-id="a82bd-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="a82bd-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a82bd-171">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="a82bd-171">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/ebsco-tutorial/tutorial_ebsco_attribute.png)

    > [!Note]
    > <span data-ttu-id="a82bd-173">The **name** attribute is mandatory and it is mapped with **User Identifier** in EBSCO application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-173">The **name** attribute is mandatory and it is mapped with **User Identifier** in EBSCO application.</span></span> <span data-ttu-id="a82bd-174">This is added by default so you don't need to add this manually.</span><span class="sxs-lookup"><span data-stu-id="a82bd-174">This is added by default so you don't need to add this manually.</span></span>
    
1. <span data-ttu-id="a82bd-175">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a82bd-175">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="a82bd-176">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="a82bd-176">Attribute Name</span></span> | <span data-ttu-id="a82bd-177">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="a82bd-177">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="a82bd-178">FirstName</span><span class="sxs-lookup"><span data-stu-id="a82bd-178">FirstName</span></span>   | <span data-ttu-id="a82bd-179">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a82bd-179">user.givenname</span></span> |
    | <span data-ttu-id="a82bd-180">LastName</span><span class="sxs-lookup"><span data-stu-id="a82bd-180">LastName</span></span>   | <span data-ttu-id="a82bd-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="a82bd-181">user.surname</span></span> |
    | <span data-ttu-id="a82bd-182">Email</span><span class="sxs-lookup"><span data-stu-id="a82bd-182">Email</span></span>   | <span data-ttu-id="a82bd-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="a82bd-183">user.mail</span></span> |

    <span data-ttu-id="a82bd-184">a.</span><span class="sxs-lookup"><span data-stu-id="a82bd-184">a.</span></span> <span data-ttu-id="a82bd-185">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="a82bd-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ebsco-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/ebsco-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a82bd-188">b.</span><span class="sxs-lookup"><span data-stu-id="a82bd-188">b.</span></span> <span data-ttu-id="a82bd-189">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a82bd-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a82bd-190">c.</span><span class="sxs-lookup"><span data-stu-id="a82bd-190">c.</span></span> <span data-ttu-id="a82bd-191">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a82bd-191">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a82bd-192">d.</span><span class="sxs-lookup"><span data-stu-id="a82bd-192">d.</span></span> <span data-ttu-id="a82bd-193">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="a82bd-193">Click **Ok**</span></span>

1. <span data-ttu-id="a82bd-194">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a82bd-194">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/ebsco-tutorial/tutorial_ebsco_certificate.png) 

1. <span data-ttu-id="a82bd-196">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a82bd-196">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ebsco-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a82bd-198">To configure single sign-on on **EBSCO** side, you need to send the downloaded **Metadata XML** to [EBSCO support team](mailto:sso@ebsco.com).</span><span class="sxs-lookup"><span data-stu-id="a82bd-198">To configure single sign-on on **EBSCO** side, you need to send the downloaded **Metadata XML** to [EBSCO support team](mailto:sso@ebsco.com).</span></span> <span data-ttu-id="a82bd-199">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a82bd-199">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a82bd-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a82bd-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a82bd-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a82bd-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a82bd-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a82bd-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a82bd-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a82bd-203">Create an Azure AD test user</span></span>

<span data-ttu-id="a82bd-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a82bd-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a82bd-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a82bd-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a82bd-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ebsco-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a82bd-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ebsco-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a82bd-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a82bd-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ebsco-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a82bd-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a82bd-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ebsco-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a82bd-215">a.</span><span class="sxs-lookup"><span data-stu-id="a82bd-215">a.</span></span> <span data-ttu-id="a82bd-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a82bd-217">b.</span><span class="sxs-lookup"><span data-stu-id="a82bd-217">b.</span></span> <span data-ttu-id="a82bd-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a82bd-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a82bd-219">c.</span><span class="sxs-lookup"><span data-stu-id="a82bd-219">c.</span></span> <span data-ttu-id="a82bd-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a82bd-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a82bd-221">d.</span><span class="sxs-lookup"><span data-stu-id="a82bd-221">d.</span></span> <span data-ttu-id="a82bd-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-222">Click **Create**.</span></span>
 
### <a name="create-an-ebsco-test-user"></a><span data-ttu-id="a82bd-223">Create an EBSCO test user</span><span class="sxs-lookup"><span data-stu-id="a82bd-223">Create an EBSCO test user</span></span>

<span data-ttu-id="a82bd-224">In the case of EBSCO, user provisioning is automatic.</span><span class="sxs-lookup"><span data-stu-id="a82bd-224">In the case of EBSCO, user provisioning is automatic.</span></span>

<span data-ttu-id="a82bd-225">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-225">**To provision a user account, perform the following steps:**</span></span>

<span data-ttu-id="a82bd-226">Azure AD passes the required data to EBSCO application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-226">Azure AD passes the required data to EBSCO application.</span></span> <span data-ttu-id="a82bd-227">EBSCO’s user provisioning can be automatic OR require a one-time form.</span><span class="sxs-lookup"><span data-stu-id="a82bd-227">EBSCO’s user provisioning can be automatic OR require a one-time form.</span></span> <span data-ttu-id="a82bd-228">It depends on whether the client has a lot of pre-existing EBSCOhost accounts with personal settings saved.</span><span class="sxs-lookup"><span data-stu-id="a82bd-228">It depends on whether the client has a lot of pre-existing EBSCOhost accounts with personal settings saved.</span></span> <span data-ttu-id="a82bd-229">The same can be discussed with the [EBSCO support team](mailto:sso@ebsco.com) during the implementation.</span><span class="sxs-lookup"><span data-stu-id="a82bd-229">The same can be discussed with the [EBSCO support team](mailto:sso@ebsco.com) during the implementation.</span></span> <span data-ttu-id="a82bd-230">Either way, the client doesn’t have to create any EBSCOhost accounts prior to testing.</span><span class="sxs-lookup"><span data-stu-id="a82bd-230">Either way, the client doesn’t have to create any EBSCOhost accounts prior to testing.</span></span>

   >[!Note]
   ><span data-ttu-id="a82bd-231">You can automate EBSCOhost user provisioning/personalization.</span><span class="sxs-lookup"><span data-stu-id="a82bd-231">You can automate EBSCOhost user provisioning/personalization.</span></span> <span data-ttu-id="a82bd-232">Contact [EBSCO support team](mailto:sso@ebsco.com) about Just-In-Time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="a82bd-232">Contact [EBSCO support team](mailto:sso@ebsco.com) about Just-In-Time user provisioning.</span></span> 
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a82bd-233">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a82bd-233">Assign the Azure AD test user</span></span>

<span data-ttu-id="a82bd-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EBSCO.</span><span class="sxs-lookup"><span data-stu-id="a82bd-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EBSCO.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a82bd-236">**To assign Britta Simon to EBSCO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a82bd-236">**To assign Britta Simon to EBSCO, perform the following steps:**</span></span>

1. <span data-ttu-id="a82bd-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a82bd-239">In the applications list, select **EBSCO**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-239">In the applications list, select **EBSCO**.</span></span>

    ![The EBSCO link in the Applications list](./media/ebsco-tutorial/tutorial_ebsco_app.png)  

1. <span data-ttu-id="a82bd-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-241">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a82bd-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a82bd-243">Click **Add** button.</span></span> <span data-ttu-id="a82bd-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a82bd-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a82bd-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a82bd-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a82bd-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a82bd-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a82bd-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a82bd-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a82bd-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a82bd-249">Test single sign-on</span></span>

<span data-ttu-id="a82bd-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a82bd-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="a82bd-251">When you click the EBSCO tile in the Access Panel, you should get automatically signed-on to your EBSCO application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-251">When you click the EBSCO tile in the Access Panel, you should get automatically signed-on to your EBSCO application.</span></span>
<span data-ttu-id="a82bd-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a82bd-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

1. <span data-ttu-id="a82bd-253">Once you login to the application, click on the **sign in** button in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="a82bd-253">Once you login to the application, click on the **sign in** button in the top right corner.</span></span>

    ![The EBSCO signin in the Applications list](./media/ebsco-tutorial/tutorial_ebsco_signin.png)
 
1. <span data-ttu-id="a82bd-255">You will receive a one-time prompt to pair the institutional/SAML login with an **Link your existing MyEBSCOhost account to your institution account now** OR **Create a new MyEBSCOhost account and link it to your institution account**.</span><span class="sxs-lookup"><span data-stu-id="a82bd-255">You will receive a one-time prompt to pair the institutional/SAML login with an **Link your existing MyEBSCOhost account to your institution account now** OR **Create a new MyEBSCOhost account and link it to your institution account**.</span></span> <span data-ttu-id="a82bd-256">The account is used for personalization on the EBSCOhost application.</span><span class="sxs-lookup"><span data-stu-id="a82bd-256">The account is used for personalization on the EBSCOhost application.</span></span> <span data-ttu-id="a82bd-257">Select the option **Create a new account** and  you will see that the form for personalization is pre-completed with the values from the saml response as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="a82bd-257">Select the option **Create a new account** and  you will see that the form for personalization is pre-completed with the values from the saml response as shown in the screenshot below.</span></span> <span data-ttu-id="a82bd-258">Click **‘Continue’** to save this selection.</span><span class="sxs-lookup"><span data-stu-id="a82bd-258">Click **‘Continue’** to save this selection.</span></span>
    
     ![The EBSCO user in the Applications list](./media/ebsco-tutorial/tutorial_ebsco_user.png)

1. <span data-ttu-id="a82bd-260">After completing the above setup, clear cookies/cache and login again.</span><span class="sxs-lookup"><span data-stu-id="a82bd-260">After completing the above setup, clear cookies/cache and login again.</span></span> <span data-ttu-id="a82bd-261">You won’t have to manually signin again and the personalization settings are remembered</span><span class="sxs-lookup"><span data-stu-id="a82bd-261">You won’t have to manually signin again and the personalization settings are remembered</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a82bd-262">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a82bd-262">Additional resources</span></span>

* [<span data-ttu-id="a82bd-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a82bd-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a82bd-264">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a82bd-264">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ebsco-tutorial/tutorial_general_01.png
[2]: ./media/ebsco-tutorial/tutorial_general_02.png
[3]: ./media/ebsco-tutorial/tutorial_general_03.png
[4]: ./media/ebsco-tutorial/tutorial_general_04.png

[100]: ./media/ebsco-tutorial/tutorial_general_100.png

[200]: ./media/ebsco-tutorial/tutorial_general_200.png
[201]: ./media/ebsco-tutorial/tutorial_general_201.png
[202]: ./media/ebsco-tutorial/tutorial_general_202.png
[203]: ./media/ebsco-tutorial/tutorial_general_203.png

