---
title: 'Tutorial: Azure Active Directory integration with Zscaler Private Access Administrator | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler Private Access Administrator.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c87392a7-e7fe-4cdc-a8e6-afe1ed975172
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2018
ms.author: jeedes
ms.openlocfilehash: 61b469ba5f64a52b87843432dfe60fe1d83ffec2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869000"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-administrator"></a><span data-ttu-id="3ba8b-103">Tutorial: Azure Active Directory integration with Zscaler Private Access Administrator</span><span class="sxs-lookup"><span data-stu-id="3ba8b-103">Tutorial: Azure Active Directory integration with Zscaler Private Access Administrator</span></span>

<span data-ttu-id="3ba8b-104">In this tutorial, you learn how to integrate Zscaler Private Access Administrator with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ba8b-104">In this tutorial, you learn how to integrate Zscaler Private Access Administrator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ba8b-105">Integrating Zscaler Private Access Administrator with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-105">Integrating Zscaler Private Access Administrator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ba8b-106">You can control in Azure AD who has access to Zscaler Private Access Administrator.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-106">You can control in Azure AD who has access to Zscaler Private Access Administrator.</span></span>
- <span data-ttu-id="3ba8b-107">You can enable your users to automatically get signed-on to Zscaler Private Access Administrator (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-107">You can enable your users to automatically get signed-on to Zscaler Private Access Administrator (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3ba8b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3ba8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3ba8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ba8b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3ba8b-110">Prerequisites</span></span>

<span data-ttu-id="3ba8b-111">To configure Azure AD integration with Zscaler Private Access Administrator, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-111">To configure Azure AD integration with Zscaler Private Access Administrator, you need the following items:</span></span>

- <span data-ttu-id="3ba8b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3ba8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ba8b-113">A Zscaler Private Access Administrator single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3ba8b-113">A Zscaler Private Access Administrator single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ba8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ba8b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ba8b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ba8b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ba8b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ba8b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3ba8b-118">Scenario description</span></span>
<span data-ttu-id="3ba8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ba8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ba8b-121">Adding Zscaler Private Access Administrator from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ba8b-121">Adding Zscaler Private Access Administrator from the gallery</span></span>
1. <span data-ttu-id="3ba8b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ba8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-private-access-administrator-from-the-gallery"></a><span data-ttu-id="3ba8b-123">Adding Zscaler Private Access Administrator from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ba8b-123">Adding Zscaler Private Access Administrator from the gallery</span></span>
<span data-ttu-id="3ba8b-124">To configure the integration of Zscaler Private Access Administrator into Azure AD, you need to add Zscaler Private Access Administrator from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-124">To configure the integration of Zscaler Private Access Administrator into Azure AD, you need to add Zscaler Private Access Administrator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ba8b-125">**To add Zscaler Private Access Administrator from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-125">**To add Zscaler Private Access Administrator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ba8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="3ba8b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ba8b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="3ba8b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="3ba8b-133">In the search box, type **Zscaler Private Access Administrator**, select **Zscaler Private Access Administrator** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-133">In the search box, type **Zscaler Private Access Administrator**, select **Zscaler Private Access Administrator** from result panel then click **Add** button to add the application.</span></span>

    ![Zscaler Private Access Administrator in the results list](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3ba8b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ba8b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3ba8b-136">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access Administrator based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ba8b-136">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access Administrator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ba8b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access Administrator is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access Administrator is to a user in Azure AD.</span></span> <span data-ttu-id="3ba8b-138">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access Administrator needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-138">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access Administrator needs to be established.</span></span>

<span data-ttu-id="3ba8b-139">To configure and test Azure AD single sign-on with Zscaler Private Access Administrator, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-139">To configure and test Azure AD single sign-on with Zscaler Private Access Administrator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ba8b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3ba8b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3ba8b-142">**[Create a Zscaler Private Access Administrator test user](#create-a-zscaler-private-access-administrator-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access Administrator that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-142">**[Create a Zscaler Private Access Administrator test user](#create-a-zscaler-private-access-administrator-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access Administrator that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3ba8b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3ba8b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3ba8b-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ba8b-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3ba8b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Private Access Administrator application.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Private Access Administrator application.</span></span>

<span data-ttu-id="3ba8b-147">**To configure Azure AD single sign-on with Zscaler Private Access Administrator, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-147">**To configure Azure AD single sign-on with Zscaler Private Access Administrator, perform the following steps:**</span></span>

1. <span data-ttu-id="3ba8b-148">In the Azure portal, on the **Zscaler Private Access Administrator** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-148">In the Azure portal, on the **Zscaler Private Access Administrator** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="3ba8b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_samlbase.png)

1. <span data-ttu-id="3ba8b-152">On the **Zscaler Private Access Administrator Domain and URLs** section if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-152">On the **Zscaler Private Access Administrator Domain and URLs** section if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Zscaler Private Access Administrator Domain and URLs single sign-on information](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_url.png)

    <span data-ttu-id="3ba8b-154">a.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-154">a.</span></span> <span data-ttu-id="3ba8b-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="3ba8b-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/metadata`</span></span>

    <span data-ttu-id="3ba8b-156">b.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-156">b.</span></span> <span data-ttu-id="3ba8b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/sso`</span><span class="sxs-lookup"><span data-stu-id="3ba8b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/sso`</span></span>

    <span data-ttu-id="3ba8b-158">c.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-158">c.</span></span> <span data-ttu-id="3ba8b-159">Check **Show advanced URL settings**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-159">Check **Show advanced URL settings**</span></span>

    <span data-ttu-id="3ba8b-160">d.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-160">d.</span></span> <span data-ttu-id="3ba8b-161">In the **RelayState** textbox, type a value: `idpadminsso`</span><span class="sxs-lookup"><span data-stu-id="3ba8b-161">In the **RelayState** textbox, type a value: `idpadminsso`</span></span>

1.  <span data-ttu-id="3ba8b-162">If you wish to configure the application in **SP** initiated mode perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-162">If you wish to configure the application in **SP** initiated mode perform the following steps:</span></span>

    <span data-ttu-id="3ba8b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/sso`</span><span class="sxs-lookup"><span data-stu-id="3ba8b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.private.zscaler.com/auth/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ba8b-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-164">These values are not real.</span></span> <span data-ttu-id="3ba8b-165">Update these values with the actual Identifier, Reply URL and Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-165">Update these values with the actual Identifier, Reply URL and Sign-on URL.</span></span> <span data-ttu-id="3ba8b-166">Contact [Zscaler Private Access Administrator support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-166">Contact [Zscaler Private Access Administrator support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>
 
1. <span data-ttu-id="3ba8b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_certificate.png) 

1. <span data-ttu-id="3ba8b-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3ba8b-171">In a different web browser window, login to Zscaler Private Access Administrator as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-171">In a different web browser window, login to Zscaler Private Access Administrator as an Administrator.</span></span>

1. <span data-ttu-id="3ba8b-172">On the top, click **Administration** and navigate to **AUTHENTICATION** section click **IdP Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-172">On the top, click **Administration** and navigate to **AUTHENTICATION** section click **IdP Configuration**.</span></span>

    ![Zscaler Private Access Administrator admin](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_admin.png)

1. <span data-ttu-id="3ba8b-174">In the top right corner, click **Add IdP Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-174">In the top right corner, click **Add IdP Configuration**.</span></span> 

    ![Zscaler Private Access Administrator addidp](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_addpidp.png)

1. <span data-ttu-id="3ba8b-176">On the **Add IdP Configuration** page perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-176">On the **Add IdP Configuration** page perform the following steps:</span></span>
 
    ![Zscaler Private Access Administrator idpselect](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_idpselect.png)

    <span data-ttu-id="3ba8b-178">a.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-178">a.</span></span> <span data-ttu-id="3ba8b-179">Click **Select File** to upload the downloaded Metadata file from Azure AD in the **IdP Metadata File Upload** field.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-179">Click **Select File** to upload the downloaded Metadata file from Azure AD in the **IdP Metadata File Upload** field.</span></span>

    <span data-ttu-id="3ba8b-180">b.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-180">b.</span></span> <span data-ttu-id="3ba8b-181">It reads the **IdP metadata** from Azure AD and populates all the fields information as shown below.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-181">It reads the **IdP metadata** from Azure AD and populates all the fields information as shown below.</span></span>

    ![Zscaler Private Access Administrator idpconfig](./media/zscalerprivateaccessadministrator-tutorial/idpconfig.png)

    <span data-ttu-id="3ba8b-183">c.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-183">c.</span></span> <span data-ttu-id="3ba8b-184">Select **Single Sign On** as **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-184">Select **Single Sign On** as **Administrator**.</span></span>

    <span data-ttu-id="3ba8b-185">d.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-185">d.</span></span> <span data-ttu-id="3ba8b-186">Select your domain from **Domains** field.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-186">Select your domain from **Domains** field.</span></span>
    
    <span data-ttu-id="3ba8b-187">e.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-187">e.</span></span> <span data-ttu-id="3ba8b-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3ba8b-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3ba8b-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ba8b-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ba8b-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ba8b-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3ba8b-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ba8b-192">Create an Azure AD test user</span></span>

<span data-ttu-id="3ba8b-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3ba8b-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ba8b-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zscalerprivateaccessadministrator-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="3ba8b-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zscalerprivateaccessadministrator-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="3ba8b-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zscalerprivateaccessadministrator-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="3ba8b-202">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-202">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zscalerprivateaccessadministrator-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3ba8b-204">a.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-204">a.</span></span> <span data-ttu-id="3ba8b-205">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ba8b-206">b.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-206">b.</span></span> <span data-ttu-id="3ba8b-207">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3ba8b-208">c.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-208">c.</span></span> <span data-ttu-id="3ba8b-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3ba8b-210">d.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-210">d.</span></span> <span data-ttu-id="3ba8b-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-211">Click **Create**.</span></span>
  
### <a name="create-a-zscaler-private-access-administrator-test-user"></a><span data-ttu-id="3ba8b-212">Create a Zscaler Private Access Administrator test user</span><span class="sxs-lookup"><span data-stu-id="3ba8b-212">Create a Zscaler Private Access Administrator test user</span></span>

<span data-ttu-id="3ba8b-213">To enable Azure AD users to log in to Zscaler Private Access Administrator, they must be provisioned into Zscaler Private Access Administrator.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-213">To enable Azure AD users to log in to Zscaler Private Access Administrator, they must be provisioned into Zscaler Private Access Administrator.</span></span> <span data-ttu-id="3ba8b-214">In the case of Zscaler Private Access Administrator, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-214">In the case of Zscaler Private Access Administrator, provisioning is a manual task.</span></span>

<span data-ttu-id="3ba8b-215">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3ba8b-216">Log in to your Zscaler Private Access Administrator company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-216">Log in to your Zscaler Private Access Administrator company site as an administrator.</span></span>

1. <span data-ttu-id="3ba8b-217">On the top, click **Administration** and navigate to **AUTHENTICATION** section click **IdP Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-217">On the top, click **Administration** and navigate to **AUTHENTICATION** section click **IdP Configuration**.</span></span>

    ![Zscaler Private Access Administrator admin](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_admin.png)

1. <span data-ttu-id="3ba8b-219">Click **Administrators** from left side of the menu.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-219">Click **Administrators** from left side of the menu.</span></span>

    ![Zscaler Private Access Administrator administrator](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_adminstrator.png)

1. <span data-ttu-id="3ba8b-221">In the top right corner, click **Add Administrator**:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-221">In the top right corner, click **Add Administrator**:</span></span>

    ![Zscaler Private Access Administrator add admin](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_addadmin.png)

1. <span data-ttu-id="3ba8b-223">In the **Add Administrator** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ba8b-223">In the **Add Administrator** page, perform the following steps:</span></span>

    ![Zscaler Private Access Administrator user admin](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_useradmin.png)

    <span data-ttu-id="3ba8b-225">a.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-225">a.</span></span> <span data-ttu-id="3ba8b-226">In the **Username** textbox, enter the email of user like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-226">In the **Username** textbox, enter the email of user like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="3ba8b-227">b.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-227">b.</span></span> <span data-ttu-id="3ba8b-228">In the **Password** textbox, type the Password.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-228">In the **Password** textbox, type the Password.</span></span>

    <span data-ttu-id="3ba8b-229">c.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-229">c.</span></span> <span data-ttu-id="3ba8b-230">In the **Confirm Password** textbox, type the Password.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-230">In the **Confirm Password** textbox, type the Password.</span></span>

    <span data-ttu-id="3ba8b-231">d.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-231">d.</span></span> <span data-ttu-id="3ba8b-232">Select **Role** as **Zscaler Private Access Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-232">Select **Role** as **Zscaler Private Access Administrator**.</span></span>

    <span data-ttu-id="3ba8b-233">e.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-233">e.</span></span> <span data-ttu-id="3ba8b-234">In the **Email** textbox, enter the email of user like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-234">In the **Email** textbox, enter the email of user like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="3ba8b-235">f.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-235">f.</span></span> <span data-ttu-id="3ba8b-236">In the **Phone** textbox, type the Phone number.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-236">In the **Phone** textbox, type the Phone number.</span></span>

    <span data-ttu-id="3ba8b-237">g.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-237">g.</span></span> <span data-ttu-id="3ba8b-238">In the **Timezone** textbox, select the Timezone.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-238">In the **Timezone** textbox, select the Timezone.</span></span>

    <span data-ttu-id="3ba8b-239">h.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-239">h.</span></span> <span data-ttu-id="3ba8b-240">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-240">Click **Save**.</span></span>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3ba8b-241">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ba8b-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="3ba8b-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Private Access Administrator.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Private Access Administrator.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3ba8b-244">**To assign Britta Simon to Zscaler Private Access Administrator, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ba8b-244">**To assign Britta Simon to Zscaler Private Access Administrator, perform the following steps:**</span></span>

1. <span data-ttu-id="3ba8b-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3ba8b-247">In the applications list, select **Zscaler Private Access Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-247">In the applications list, select **Zscaler Private Access Administrator**.</span></span>

    ![The Zscaler Private Access Administrator link in the Applications list](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_app.png)  

1. <span data-ttu-id="3ba8b-249">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-249">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="3ba8b-251">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-251">Click **Add** button.</span></span> <span data-ttu-id="3ba8b-252">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="3ba8b-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3ba8b-255">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-255">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3ba8b-256">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3ba8b-257">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ba8b-257">Test single sign-on</span></span>

<span data-ttu-id="3ba8b-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ba8b-259">When you click the Zscaler Private Access Administrator tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access Administrator application.</span><span class="sxs-lookup"><span data-stu-id="3ba8b-259">When you click the Zscaler Private Access Administrator tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access Administrator application.</span></span>
<span data-ttu-id="3ba8b-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ba8b-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ba8b-261">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3ba8b-261">Additional resources</span></span>

* [<span data-ttu-id="3ba8b-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ba8b-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3ba8b-263">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ba8b-263">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_01.png
[2]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_02.png
[3]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_03.png
[4]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_04.png

[100]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_100.png

[200]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_200.png
[201]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_201.png
[202]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_202.png
[203]: ./media/zscalerprivateaccessadministrator-tutorial/tutorial_general_203.png

