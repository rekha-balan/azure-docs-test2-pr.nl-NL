---
title: 'Tutorial: Azure Active Directory integration with Qumu Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Qumu Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d8c4a97b-4de6-49d4-b64e-42222c2ec6c9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2018
ms.author: jeedes
ms.openlocfilehash: 1e42d83ed7f74b366d2bca248a794cc9fb506b73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857600"
---
# <a name="tutorial-azure-active-directory-integration-with-qumu-cloud"></a><span data-ttu-id="9b2cc-103">Tutorial: Azure Active Directory integration with Qumu Cloud</span><span class="sxs-lookup"><span data-stu-id="9b2cc-103">Tutorial: Azure Active Directory integration with Qumu Cloud</span></span>

<span data-ttu-id="9b2cc-104">In this tutorial, you learn how to integrate Qumu Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-104">In this tutorial, you learn how to integrate Qumu Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b2cc-105">Integrating Qumu Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-105">Integrating Qumu Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b2cc-106">You can control in Azure AD who has access to Qumu Cloud.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-106">You can control in Azure AD who has access to Qumu Cloud.</span></span>
- <span data-ttu-id="9b2cc-107">You can enable your users to automatically get signed-on to Qumu Cloud (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-107">You can enable your users to automatically get signed-on to Qumu Cloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9b2cc-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9b2cc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2cc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9b2cc-110">Prerequisites</span></span>

<span data-ttu-id="9b2cc-111">To configure Azure AD integration with Qumu Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-111">To configure Azure AD integration with Qumu Cloud, you need the following items:</span></span>

- <span data-ttu-id="9b2cc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9b2cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b2cc-113">A Qumu Cloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9b2cc-113">A Qumu Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b2cc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b2cc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b2cc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b2cc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b2cc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9b2cc-118">Scenario description</span></span>
<span data-ttu-id="9b2cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b2cc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b2cc-121">Adding Qumu Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b2cc-121">Adding Qumu Cloud from the gallery</span></span>
1. <span data-ttu-id="9b2cc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b2cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qumu-cloud-from-the-gallery"></a><span data-ttu-id="9b2cc-123">Adding Qumu Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b2cc-123">Adding Qumu Cloud from the gallery</span></span>
<span data-ttu-id="9b2cc-124">To configure the integration of Qumu Cloud into Azure AD, you need to add Qumu Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-124">To configure the integration of Qumu Cloud into Azure AD, you need to add Qumu Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b2cc-125">**To add Qumu Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b2cc-125">**To add Qumu Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2cc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9b2cc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b2cc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="9b2cc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9b2cc-133">In the search box, type **Qumu Cloud**, select **Qumu Cloud** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-133">In the search box, type **Qumu Cloud**, select **Qumu Cloud** from result panel then click **Add** button to add the application.</span></span>

    ![Qumu Cloud in the results list](./media/qumucloud-tutorial/tutorial_qumucloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9b2cc-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b2cc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9b2cc-136">In this section, you configure and test Azure AD single sign-on with Qumu Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9b2cc-136">In this section, you configure and test Azure AD single sign-on with Qumu Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b2cc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qumu Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qumu Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="9b2cc-138">In other words, a link relationship between an Azure AD user and the related user in Qumu Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-138">In other words, a link relationship between an Azure AD user and the related user in Qumu Cloud needs to be established.</span></span>

<span data-ttu-id="9b2cc-139">To configure and test Azure AD single sign-on with Qumu Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-139">To configure and test Azure AD single sign-on with Qumu Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b2cc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9b2cc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9b2cc-142">**[Create a Qumu Cloud test user](#create-a-qumu-cloud-test-user)** - to have a counterpart of Britta Simon in Qumu Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-142">**[Create a Qumu Cloud test user](#create-a-qumu-cloud-test-user)** - to have a counterpart of Britta Simon in Qumu Cloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9b2cc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9b2cc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9b2cc-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b2cc-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9b2cc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qumu Cloud application.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qumu Cloud application.</span></span>

<span data-ttu-id="9b2cc-147">**To configure Azure AD single sign-on with Qumu Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b2cc-147">**To configure Azure AD single sign-on with Qumu Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2cc-148">In the Azure portal, on the **Qumu Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-148">In the Azure portal, on the **Qumu Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="9b2cc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/qumucloud-tutorial/tutorial_qumucloud_samlbase.png)

1. <span data-ttu-id="9b2cc-152">On the **Qumu Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-152">On the **Qumu Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Qumu Cloud Domain and URLs single sign-on information](./media/qumucloud-tutorial/tutorial_qumucloud_url.png)

    <span data-ttu-id="9b2cc-154">a.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-154">a.</span></span> <span data-ttu-id="9b2cc-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="9b2cc-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com/saml/SSO`</span></span>

    <span data-ttu-id="9b2cc-156">b.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-156">b.</span></span> <span data-ttu-id="9b2cc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="9b2cc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com/saml/SSO`</span></span>

1. <span data-ttu-id="9b2cc-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Qumu Cloud Domain and URLs single sign-on information](./media/qumucloud-tutorial/tutorial_qumucloud_url1.png)

    <span data-ttu-id="9b2cc-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com`</span><span class="sxs-lookup"><span data-stu-id="9b2cc-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.qumucloud.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9b2cc-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-161">These values are not real.</span></span> <span data-ttu-id="9b2cc-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9b2cc-163">Contact [Qumu Cloud Client support team](mailto:support@qumu.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-163">Contact [Qumu Cloud Client support team](mailto:support@qumu.com) to get these values.</span></span>

1. <span data-ttu-id="9b2cc-164">Qumu Cloud application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-164">Qumu Cloud application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9b2cc-165">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="9b2cc-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9b2cc-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-167">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/qumucloud-tutorial/attribute.png)
    
1. <span data-ttu-id="9b2cc-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="9b2cc-170">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="9b2cc-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="9b2cc-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="9b2cc-171">Attribute Name</span></span> | <span data-ttu-id="9b2cc-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="9b2cc-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="9b2cc-173">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="9b2cc-173">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="9b2cc-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9b2cc-174">user.givenname</span></span> |
    | <span data-ttu-id="9b2cc-175">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="9b2cc-175">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="9b2cc-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="9b2cc-176">user.surname</span></span> |
    | <span data-ttu-id="9b2cc-177">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="9b2cc-177">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="9b2cc-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="9b2cc-178">user.mail</span></span> |
    | <span data-ttu-id="9b2cc-179">urn:oid:0.9.2342.19200300.100.1.1</span><span class="sxs-lookup"><span data-stu-id="9b2cc-179">urn:oid:0.9.2342.19200300.100.1.1</span></span> | <span data-ttu-id="9b2cc-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9b2cc-180">user.userprincipalname</span></span> |

    <span data-ttu-id="9b2cc-181">a.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-181">a.</span></span> <span data-ttu-id="9b2cc-182">Click the attribute to open the **Edit Attribute** window.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Configure Single Sign-On](./media/qumucloud-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="9b2cc-184">b.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-184">b.</span></span> <span data-ttu-id="9b2cc-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configure Single Sign-On](./media/qumucloud-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9b2cc-187">c.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-187">c.</span></span> <span data-ttu-id="9b2cc-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-188">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="9b2cc-189">d.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-189">d.</span></span> <span data-ttu-id="9b2cc-190">Keep the **Namespace** textbox blank.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-190">Keep the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="9b2cc-191">e.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-191">e.</span></span> <span data-ttu-id="9b2cc-192">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-192">Click **Ok**.</span></span>

1. <span data-ttu-id="9b2cc-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/qumucloud-tutorial/tutorial_qumucloud_certificate.png) 

1. <span data-ttu-id="9b2cc-195">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-195">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/qumucloud-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="9b2cc-197">To configure single sign-on on **Qumu Cloud** side, you need to send the downloaded **Metadata XML** to [Qumu Cloud support team](mailto:support@qumu.com).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-197">To configure single sign-on on **Qumu Cloud** side, you need to send the downloaded **Metadata XML** to [Qumu Cloud support team](mailto:support@qumu.com).</span></span> <span data-ttu-id="9b2cc-198">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-198">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9b2cc-199">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9b2cc-199">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b2cc-200">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-200">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b2cc-201">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b2cc-201">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9b2cc-202">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b2cc-202">Create an Azure AD test user</span></span>

<span data-ttu-id="9b2cc-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9b2cc-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b2cc-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2cc-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/qumucloud-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9b2cc-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/qumucloud-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9b2cc-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/qumucloud-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9b2cc-212">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b2cc-212">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/qumucloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9b2cc-214">a.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-214">a.</span></span> <span data-ttu-id="9b2cc-215">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-215">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b2cc-216">b.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-216">b.</span></span> <span data-ttu-id="9b2cc-217">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-217">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9b2cc-218">c.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-218">c.</span></span> <span data-ttu-id="9b2cc-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9b2cc-220">d.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-220">d.</span></span> <span data-ttu-id="9b2cc-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-221">Click **Create**.</span></span>
 
### <a name="create-a-qumu-cloud-test-user"></a><span data-ttu-id="9b2cc-222">Create a Qumu Cloud test user</span><span class="sxs-lookup"><span data-stu-id="9b2cc-222">Create a Qumu Cloud test user</span></span>

<span data-ttu-id="9b2cc-223">The objective of this section is to create a user called Britta Simon in Qumu Cloud.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-223">The objective of this section is to create a user called Britta Simon in Qumu Cloud.</span></span> <span data-ttu-id="9b2cc-224">Qumu Cloud supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-224">Qumu Cloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9b2cc-225">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-225">There is no action item for you in this section.</span></span> <span data-ttu-id="9b2cc-226">A new user is created during an attempt to access Qumu Cloud if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-226">A new user is created during an attempt to access Qumu Cloud if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="9b2cc-227">If you need to create a user manually, contact [Qumu Cloud Client support team](mailto:support@qumu.com).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-227">If you need to create a user manually, contact [Qumu Cloud Client support team](mailto:support@qumu.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9b2cc-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b2cc-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="9b2cc-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qumu Cloud.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qumu Cloud.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9b2cc-231">**To assign Britta Simon to Qumu Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b2cc-231">**To assign Britta Simon to Qumu Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2cc-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9b2cc-234">In the applications list, select **Qumu Cloud**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-234">In the applications list, select **Qumu Cloud**.</span></span>

    ![The Qumu Cloud link in the Applications list](./media/qumucloud-tutorial/tutorial_qumucloud_app.png)  

1. <span data-ttu-id="9b2cc-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9b2cc-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-238">Click **Add** button.</span></span> <span data-ttu-id="9b2cc-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9b2cc-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9b2cc-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9b2cc-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9b2cc-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b2cc-244">Test single sign-on</span></span>

<span data-ttu-id="9b2cc-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b2cc-246">When you click the Qumu Cloud tile in the Access Panel, you should get automatically signed-on to your Qumu Cloud application.</span><span class="sxs-lookup"><span data-stu-id="9b2cc-246">When you click the Qumu Cloud tile in the Access Panel, you should get automatically signed-on to your Qumu Cloud application.</span></span>
<span data-ttu-id="9b2cc-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b2cc-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b2cc-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9b2cc-248">Additional resources</span></span>

* [<span data-ttu-id="9b2cc-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b2cc-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9b2cc-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b2cc-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/qumucloud-tutorial/tutorial_general_01.png
[2]: ./media/qumucloud-tutorial/tutorial_general_02.png
[3]: ./media/qumucloud-tutorial/tutorial_general_03.png
[4]: ./media/qumucloud-tutorial/tutorial_general_04.png

[100]: ./media/qumucloud-tutorial/tutorial_general_100.png

[200]: ./media/qumucloud-tutorial/tutorial_general_200.png
[201]: ./media/qumucloud-tutorial/tutorial_general_201.png
[202]: ./media/qumucloud-tutorial/tutorial_general_202.png
[203]: ./media/qumucloud-tutorial/tutorial_general_203.png

