---
title: 'Tutorial: Azure Active Directory integration with iPass SmartConnect | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and iPass SmartConnect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: dee6d039-f9bb-49a2-a408-5ed40ef17d9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: ecfdd3fae1d394e3b57fcd325f44cad0d1a98534
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965716"
---
# <a name="tutorial-azure-active-directory-integration-with-ipass-smartconnect"></a><span data-ttu-id="73c68-103">Tutorial: Azure Active Directory integration with iPass SmartConnect</span><span class="sxs-lookup"><span data-stu-id="73c68-103">Tutorial: Azure Active Directory integration with iPass SmartConnect</span></span>

<span data-ttu-id="73c68-104">In this tutorial, you learn how to integrate iPass SmartConnect with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73c68-104">In this tutorial, you learn how to integrate iPass SmartConnect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73c68-105">Integrating iPass SmartConnect with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="73c68-105">Integrating iPass SmartConnect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73c68-106">You can control in Azure AD who has access to iPass SmartConnect.</span><span class="sxs-lookup"><span data-stu-id="73c68-106">You can control in Azure AD who has access to iPass SmartConnect.</span></span>
- <span data-ttu-id="73c68-107">You can enable your users to automatically get signed-on to iPass SmartConnect (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="73c68-107">You can enable your users to automatically get signed-on to iPass SmartConnect (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="73c68-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="73c68-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="73c68-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="73c68-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73c68-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="73c68-110">Prerequisites</span></span>

<span data-ttu-id="73c68-111">To configure Azure AD integration with iPass SmartConnect, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="73c68-111">To configure Azure AD integration with iPass SmartConnect, you need the following items:</span></span>

- <span data-ttu-id="73c68-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="73c68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73c68-113">An iPass SmartConnect single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="73c68-113">An iPass SmartConnect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73c68-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="73c68-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73c68-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="73c68-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73c68-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="73c68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73c68-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73c68-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73c68-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="73c68-118">Scenario description</span></span>
<span data-ttu-id="73c68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="73c68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73c68-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="73c68-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73c68-121">Adding iPass SmartConnect from the gallery</span><span class="sxs-lookup"><span data-stu-id="73c68-121">Adding iPass SmartConnect from the gallery</span></span>
1. <span data-ttu-id="73c68-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73c68-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ipass-smartconnect-from-the-gallery"></a><span data-ttu-id="73c68-123">Adding iPass SmartConnect from the gallery</span><span class="sxs-lookup"><span data-stu-id="73c68-123">Adding iPass SmartConnect from the gallery</span></span>
<span data-ttu-id="73c68-124">To configure the integration of iPass SmartConnect into Azure AD, you need to add iPass SmartConnect from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="73c68-124">To configure the integration of iPass SmartConnect into Azure AD, you need to add iPass SmartConnect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73c68-125">**To add iPass SmartConnect from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-125">**To add iPass SmartConnect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73c68-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="73c68-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="73c68-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="73c68-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73c68-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73c68-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="73c68-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="73c68-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="73c68-133">In the search box, type **iPass SmartConnect**, select **iPass SmartConnect** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="73c68-133">In the search box, type **iPass SmartConnect**, select **iPass SmartConnect** from result panel then click **Add** button to add the application.</span></span>

    ![iPass SmartConnect in the results list](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="73c68-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73c68-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="73c68-136">In this section, you configure and test Azure AD single sign-on with iPass SmartConnect based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="73c68-136">In this section, you configure and test Azure AD single sign-on with iPass SmartConnect based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73c68-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iPass SmartConnect is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73c68-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iPass SmartConnect is to a user in Azure AD.</span></span> <span data-ttu-id="73c68-138">In other words, a link relationship between an Azure AD user and the related user in iPass SmartConnect needs to be established.</span><span class="sxs-lookup"><span data-stu-id="73c68-138">In other words, a link relationship between an Azure AD user and the related user in iPass SmartConnect needs to be established.</span></span>

<span data-ttu-id="73c68-139">To configure and test Azure AD single sign-on with iPass SmartConnect, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="73c68-139">To configure and test Azure AD single sign-on with iPass SmartConnect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73c68-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="73c68-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="73c68-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73c68-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="73c68-142">**[Create an iPass SmartConnect test user](#create-an-ipass-smartconnect-test-user)** - to have a counterpart of Britta Simon in iPass SmartConnect that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="73c68-142">**[Create an iPass SmartConnect test user](#create-an-ipass-smartconnect-test-user)** - to have a counterpart of Britta Simon in iPass SmartConnect that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="73c68-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73c68-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="73c68-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="73c68-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="73c68-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="73c68-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="73c68-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iPass SmartConnect application.</span><span class="sxs-lookup"><span data-stu-id="73c68-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iPass SmartConnect application.</span></span>

<span data-ttu-id="73c68-147">**To configure Azure AD single sign-on with iPass SmartConnect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-147">**To configure Azure AD single sign-on with iPass SmartConnect, perform the following steps:**</span></span>

1. <span data-ttu-id="73c68-148">In the Azure portal, on the **iPass SmartConnect** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="73c68-148">In the Azure portal, on the **iPass SmartConnect** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="73c68-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73c68-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_samlbase.png)

1. <span data-ttu-id="73c68-152">On the **iPass SmartConnect Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, no need to perform any steps.</span><span class="sxs-lookup"><span data-stu-id="73c68-152">On the **iPass SmartConnect Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, no need to perform any steps.</span></span>

    ![iPass SmartConnect Domain and URLs single sign-on information](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_url1.png)

1. <span data-ttu-id="73c68-154">Check Show advanced URL settings and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="73c68-154">Check Show advanced URL settings and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![iPass SmartConnect Domain and URLs single sign-on information](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_url2.png)

    <span data-ttu-id="73c68-156">In the Sign-on URL textbox, type a URL: `https://om-activation.ipass.com/ClientActivation/ssolanding.go`</span><span class="sxs-lookup"><span data-stu-id="73c68-156">In the Sign-on URL textbox, type a URL: `https://om-activation.ipass.com/ClientActivation/ssolanding.go`</span></span>

1. <span data-ttu-id="73c68-157">iPass SmartConnect application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="73c68-157">iPass SmartConnect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="73c68-158">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="73c68-158">Please configure the following claims for this application.</span></span> <span data-ttu-id="73c68-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="73c68-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="73c68-160">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="73c68-160">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/ipasssmartconnect-tutorial/attribute.png)

1. <span data-ttu-id="73c68-162">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="73c68-162">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="73c68-163">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="73c68-163">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="73c68-164">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="73c68-164">Attribute Name</span></span> | <span data-ttu-id="73c68-165">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="73c68-165">Attribute Value</span></span> | <span data-ttu-id="73c68-166">Namespace Value</span><span class="sxs-lookup"><span data-stu-id="73c68-166">Namespace Value</span></span>|
    | ---------------| --------------- |----------------|
    | <span data-ttu-id="73c68-167">firstName</span><span class="sxs-lookup"><span data-stu-id="73c68-167">firstName</span></span> | <span data-ttu-id="73c68-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="73c68-168">user.givenname</span></span> |   |
    | <span data-ttu-id="73c68-169">lastName</span><span class="sxs-lookup"><span data-stu-id="73c68-169">lastName</span></span> | <span data-ttu-id="73c68-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="73c68-170">user.surname</span></span> | |
    | <span data-ttu-id="73c68-171">email</span><span class="sxs-lookup"><span data-stu-id="73c68-171">email</span></span> | <span data-ttu-id="73c68-172">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="73c68-172">user.userprincipalname</span></span> | |
    | <span data-ttu-id="73c68-173">username</span><span class="sxs-lookup"><span data-stu-id="73c68-173">username</span></span> | <span data-ttu-id="73c68-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="73c68-174">user.userprincipalname</span></span> | |

    <span data-ttu-id="73c68-175">a.</span><span class="sxs-lookup"><span data-stu-id="73c68-175">a.</span></span> <span data-ttu-id="73c68-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="73c68-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ipasssmartconnect-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/ipasssmartconnect-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="73c68-179">b.</span><span class="sxs-lookup"><span data-stu-id="73c68-179">b.</span></span> <span data-ttu-id="73c68-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="73c68-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="73c68-181">c.</span><span class="sxs-lookup"><span data-stu-id="73c68-181">c.</span></span> <span data-ttu-id="73c68-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="73c68-182">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="73c68-183">d.</span><span class="sxs-lookup"><span data-stu-id="73c68-183">d.</span></span> <span data-ttu-id="73c68-184">Keep namespace value blank for that row.</span><span class="sxs-lookup"><span data-stu-id="73c68-184">Keep namespace value blank for that row.</span></span>

    <span data-ttu-id="73c68-185">e.</span><span class="sxs-lookup"><span data-stu-id="73c68-185">e.</span></span> <span data-ttu-id="73c68-186">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="73c68-186">Click **Ok**.</span></span>

1. <span data-ttu-id="73c68-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="73c68-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_certificate.png)

1. <span data-ttu-id="73c68-189">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="73c68-189">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ipasssmartconnect-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="73c68-191">To configure single sign-on on **iPass SmartConnect** side, you need to send the downloaded **Metadata XML** and your **Domain name** to [iPass SmartConnect support team](mailto:help@ipass.com).</span><span class="sxs-lookup"><span data-stu-id="73c68-191">To configure single sign-on on **iPass SmartConnect** side, you need to send the downloaded **Metadata XML** and your **Domain name** to [iPass SmartConnect support team](mailto:help@ipass.com).</span></span> <span data-ttu-id="73c68-192">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="73c68-192">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="73c68-193">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73c68-193">Create an Azure AD test user</span></span>

<span data-ttu-id="73c68-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73c68-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="73c68-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73c68-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="73c68-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ipasssmartconnect-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="73c68-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="73c68-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ipasssmartconnect-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="73c68-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="73c68-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ipasssmartconnect-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="73c68-203">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="73c68-203">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ipasssmartconnect-tutorial/create_aaduser_04.png)

    <span data-ttu-id="73c68-205">a.</span><span class="sxs-lookup"><span data-stu-id="73c68-205">a.</span></span> <span data-ttu-id="73c68-206">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73c68-206">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73c68-207">b.</span><span class="sxs-lookup"><span data-stu-id="73c68-207">b.</span></span> <span data-ttu-id="73c68-208">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73c68-208">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="73c68-209">c.</span><span class="sxs-lookup"><span data-stu-id="73c68-209">c.</span></span> <span data-ttu-id="73c68-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="73c68-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="73c68-211">d.</span><span class="sxs-lookup"><span data-stu-id="73c68-211">d.</span></span> <span data-ttu-id="73c68-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="73c68-212">Click **Create**.</span></span>

### <a name="create-an-ipass-smartconnect-test-user"></a><span data-ttu-id="73c68-213">Create an iPass SmartConnect test user</span><span class="sxs-lookup"><span data-stu-id="73c68-213">Create an iPass SmartConnect test user</span></span>

<span data-ttu-id="73c68-214">In this section, you create a user called Britta Simon in iPass SmartConnect.</span><span class="sxs-lookup"><span data-stu-id="73c68-214">In this section, you create a user called Britta Simon in iPass SmartConnect.</span></span> <span data-ttu-id="73c68-215">Work with [iPass SmartConnect support team](mailto:help@ipass.com) to add the users or the domain which is needed to be whitelisted in the iPass SmartConnect platform.</span><span class="sxs-lookup"><span data-stu-id="73c68-215">Work with [iPass SmartConnect support team](mailto:help@ipass.com) to add the users or the domain which is needed to be whitelisted in the iPass SmartConnect platform.</span></span> <span data-ttu-id="73c68-216">If the domain is added by the team, users will get automatically provisioned to the iPass SmartConnect platform.</span><span class="sxs-lookup"><span data-stu-id="73c68-216">If the domain is added by the team, users will get automatically provisioned to the iPass SmartConnect platform.</span></span> <span data-ttu-id="73c68-217">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73c68-217">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="73c68-218">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="73c68-218">Assign the Azure AD test user</span></span>

<span data-ttu-id="73c68-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iPass SmartConnect.</span><span class="sxs-lookup"><span data-stu-id="73c68-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iPass SmartConnect.</span></span>

![Assign the user role][200]

<span data-ttu-id="73c68-221">**To assign Britta Simon to iPass SmartConnect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-221">**To assign Britta Simon to iPass SmartConnect, perform the following steps:**</span></span>

1. <span data-ttu-id="73c68-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="73c68-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="73c68-224">In the applications list, select **iPass SmartConnect**.</span><span class="sxs-lookup"><span data-stu-id="73c68-224">In the applications list, select **iPass SmartConnect**.</span></span>

    ![The iPass SmartConnect link in the Applications list](./media/ipasssmartconnect-tutorial/tutorial_ipasssmartconnect_app.png)  

1. <span data-ttu-id="73c68-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="73c68-226">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="73c68-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="73c68-228">Click **Add** button.</span></span> <span data-ttu-id="73c68-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73c68-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="73c68-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="73c68-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="73c68-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="73c68-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="73c68-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="73c68-233">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="73c68-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="73c68-234">Test single sign-on</span></span>

<span data-ttu-id="73c68-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="73c68-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73c68-236">**To test the application in the SP Initiated flow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-236">**To test the application in the SP Initiated flow, perform the following steps:**</span></span>

<span data-ttu-id="73c68-237">a.</span><span class="sxs-lookup"><span data-stu-id="73c68-237">a.</span></span> <span data-ttu-id="73c68-238">Download windows iPass SmartConnect client [here](https://om-activation.ipass.com/ClientActivation/ssolanding.go).</span><span class="sxs-lookup"><span data-stu-id="73c68-238">Download windows iPass SmartConnect client [here](https://om-activation.ipass.com/ClientActivation/ssolanding.go).</span></span>

![The iPass SmartConnect link in the Applications list](./media/ipasssmartconnect-tutorial/testing3.png)

<span data-ttu-id="73c68-240">b.</span><span class="sxs-lookup"><span data-stu-id="73c68-240">b.</span></span> <span data-ttu-id="73c68-241">Install the client and launch.</span><span class="sxs-lookup"><span data-stu-id="73c68-241">Install the client and launch.</span></span>

<span data-ttu-id="73c68-242">c.</span><span class="sxs-lookup"><span data-stu-id="73c68-242">c.</span></span> <span data-ttu-id="73c68-243">Click on **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="73c68-243">Click on **Get Started**.</span></span>

![The iPass SmartConnect link in the Applications list](./media/ipasssmartconnect-tutorial/testing1.png) 

<span data-ttu-id="73c68-245">d.</span><span class="sxs-lookup"><span data-stu-id="73c68-245">d.</span></span> <span data-ttu-id="73c68-246">Enter Azure user name with domain.</span><span class="sxs-lookup"><span data-stu-id="73c68-246">Enter Azure user name with domain.</span></span> <span data-ttu-id="73c68-247">Click on **Continue**.</span><span class="sxs-lookup"><span data-stu-id="73c68-247">Click on **Continue**.</span></span> <span data-ttu-id="73c68-248">This will be redirected to Azure login page</span><span class="sxs-lookup"><span data-stu-id="73c68-248">This will be redirected to Azure login page</span></span>

![The iPass SmartConnect link in the Applications list](./media/ipasssmartconnect-tutorial/testing2.png) 

<span data-ttu-id="73c68-250">e.</span><span class="sxs-lookup"><span data-stu-id="73c68-250">e.</span></span> <span data-ttu-id="73c68-251">After successful authentication, client activation will be started.</span><span class="sxs-lookup"><span data-stu-id="73c68-251">After successful authentication, client activation will be started.</span></span> <span data-ttu-id="73c68-252">Client will get activated.</span><span class="sxs-lookup"><span data-stu-id="73c68-252">Client will get activated.</span></span>

<span data-ttu-id="73c68-253">**To test the application in the IdP Initiated flow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="73c68-253">**To test the application in the IdP Initiated flow, perform the following steps:**</span></span>

<span data-ttu-id="73c68-254">a.</span><span class="sxs-lookup"><span data-stu-id="73c68-254">a.</span></span> <span data-ttu-id="73c68-255">Login to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="73c68-255">Login to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

<span data-ttu-id="73c68-256">b.</span><span class="sxs-lookup"><span data-stu-id="73c68-256">b.</span></span> <span data-ttu-id="73c68-257">Click on iPass SmartConnect app.</span><span class="sxs-lookup"><span data-stu-id="73c68-257">Click on iPass SmartConnect app.</span></span>

<span data-ttu-id="73c68-258">c.</span><span class="sxs-lookup"><span data-stu-id="73c68-258">c.</span></span> <span data-ttu-id="73c68-259">It launches SSA page, click on **Download App for Windows** to install iPass SmartConnect client.</span><span class="sxs-lookup"><span data-stu-id="73c68-259">It launches SSA page, click on **Download App for Windows** to install iPass SmartConnect client.</span></span>

![The iPass SmartConnect link in the Applications list](./media/ipasssmartconnect-tutorial/testing4.png)

<span data-ttu-id="73c68-261">d.</span><span class="sxs-lookup"><span data-stu-id="73c68-261">d.</span></span> <span data-ttu-id="73c68-262">After installation, client on the first launch will automatically starts activation after accepting terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="73c68-262">After installation, client on the first launch will automatically starts activation after accepting terms and conditions.</span></span>

<span data-ttu-id="73c68-263">e.</span><span class="sxs-lookup"><span data-stu-id="73c68-263">e.</span></span> <span data-ttu-id="73c68-264">If activation does not start, click on Activate button on SSA page to initiate activation.</span><span class="sxs-lookup"><span data-stu-id="73c68-264">If activation does not start, click on Activate button on SSA page to initiate activation.</span></span>

<span data-ttu-id="73c68-265">f.</span><span class="sxs-lookup"><span data-stu-id="73c68-265">f.</span></span> <span data-ttu-id="73c68-266">Client will get activated.</span><span class="sxs-lookup"><span data-stu-id="73c68-266">Client will get activated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73c68-267">Additional resources</span><span class="sxs-lookup"><span data-stu-id="73c68-267">Additional resources</span></span>

* [<span data-ttu-id="73c68-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73c68-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="73c68-269">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73c68-269">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ipasssmartconnect-tutorial/tutorial_general_01.png
[2]: ./media/ipasssmartconnect-tutorial/tutorial_general_02.png
[3]: ./media/ipasssmartconnect-tutorial/tutorial_general_03.png
[4]: ./media/ipasssmartconnect-tutorial/tutorial_general_04.png

[100]: ./media/ipasssmartconnect-tutorial/tutorial_general_100.png

[200]: ./media/ipasssmartconnect-tutorial/tutorial_general_200.png
[201]: ./media/ipasssmartconnect-tutorial/tutorial_general_201.png
[202]: ./media/ipasssmartconnect-tutorial/tutorial_general_202.png
[203]: ./media/ipasssmartconnect-tutorial/tutorial_general_203.png

