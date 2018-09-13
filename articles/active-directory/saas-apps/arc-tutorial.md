---
title: 'Tutorial: Azure Active Directory integration with Arc Publishing - SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Arc Publishing - SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ae609583-f875-4cb8-b68e-1b0b7938e9a7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2018
ms.author: jeedes
ms.openlocfilehash: eafd7998e5bc21a539b6709794fe3cd70d9e3179
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965561"
---
# <a name="tutorial-azure-active-directory-integration-with-arc-publishing---sso"></a><span data-ttu-id="7b659-103">Tutorial: Azure Active Directory integration with Arc Publishing - SSO</span><span class="sxs-lookup"><span data-stu-id="7b659-103">Tutorial: Azure Active Directory integration with Arc Publishing - SSO</span></span>

<span data-ttu-id="7b659-104">In this tutorial, you learn how to integrate Arc Publishing - SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b659-104">In this tutorial, you learn how to integrate Arc Publishing - SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b659-105">Integrating Arc Publishing - SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7b659-105">Integrating Arc Publishing - SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b659-106">You can control in Azure AD who has access to Arc Publishing - SSO.</span><span class="sxs-lookup"><span data-stu-id="7b659-106">You can control in Azure AD who has access to Arc Publishing - SSO.</span></span>
- <span data-ttu-id="7b659-107">You can enable your users to automatically get signed-on to Arc Publishing - SSO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7b659-107">You can enable your users to automatically get signed-on to Arc Publishing - SSO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7b659-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b659-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7b659-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7b659-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b659-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7b659-110">Prerequisites</span></span>

<span data-ttu-id="7b659-111">To configure Azure AD integration with Arc Publishing - SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7b659-111">To configure Azure AD integration with Arc Publishing - SSO, you need the following items:</span></span>

- <span data-ttu-id="7b659-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7b659-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b659-113">An Arc Publishing - SSO single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7b659-113">An Arc Publishing - SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b659-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7b659-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b659-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7b659-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b659-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7b659-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b659-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b659-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b659-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7b659-118">Scenario description</span></span>
<span data-ttu-id="7b659-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7b659-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b659-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7b659-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b659-121">Adding Arc Publishing - SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="7b659-121">Adding Arc Publishing - SSO from the gallery</span></span>
1. <span data-ttu-id="7b659-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b659-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arc-publishing---sso-from-the-gallery"></a><span data-ttu-id="7b659-123">Adding Arc Publishing - SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="7b659-123">Adding Arc Publishing - SSO from the gallery</span></span>
<span data-ttu-id="7b659-124">To configure the integration of Arc Publishing - SSO into Azure AD, you need to add Arc Publishing - SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7b659-124">To configure the integration of Arc Publishing - SSO into Azure AD, you need to add Arc Publishing - SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b659-125">**To add Arc Publishing - SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b659-125">**To add Arc Publishing - SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b659-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7b659-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="7b659-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7b659-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b659-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7b659-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="7b659-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7b659-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="7b659-133">In the search box, type **Arc Publishing - SSO**, select **Arc Publishing - SSO** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7b659-133">In the search box, type **Arc Publishing - SSO**, select **Arc Publishing - SSO** from result panel then click **Add** button to add the application.</span></span>

    ![Arc Publishing - SSO in the results list](./media/arc-tutorial/tutorial_arc_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b659-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b659-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7b659-136">In this section, you configure and test Azure AD single sign-on with Arc Publishing - SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7b659-136">In this section, you configure and test Azure AD single sign-on with Arc Publishing - SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b659-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Arc Publishing - SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b659-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Arc Publishing - SSO is to a user in Azure AD.</span></span> <span data-ttu-id="7b659-138">In other words, a link relationship between an Azure AD user and the related user in Arc Publishing - SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7b659-138">In other words, a link relationship between an Azure AD user and the related user in Arc Publishing - SSO needs to be established.</span></span>

<span data-ttu-id="7b659-139">To configure and test Azure AD single sign-on with Arc Publishing - SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7b659-139">To configure and test Azure AD single sign-on with Arc Publishing - SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b659-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7b659-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7b659-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b659-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7b659-142">**[Create an Arc Publishing - SSO test user](#create-an-arc-publishing---sso-test-user)** - to have a counterpart of Britta Simon in Arc Publishing - SSO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7b659-142">**[Create an Arc Publishing - SSO test user](#create-an-arc-publishing---sso-test-user)** - to have a counterpart of Britta Simon in Arc Publishing - SSO that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7b659-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7b659-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7b659-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7b659-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b659-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b659-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b659-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Arc Publishing - SSO application.</span><span class="sxs-lookup"><span data-stu-id="7b659-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Arc Publishing - SSO application.</span></span>

<span data-ttu-id="7b659-147">**To configure Azure AD single sign-on with Arc Publishing - SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b659-147">**To configure Azure AD single sign-on with Arc Publishing - SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="7b659-148">In the Azure portal, on the **Arc Publishing - SSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7b659-148">In the Azure portal, on the **Arc Publishing - SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="7b659-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7b659-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/arc-tutorial/tutorial_arc_samlbase.png)

1. <span data-ttu-id="7b659-152">On the **Arc Publishing - SSO Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7b659-152">On the **Arc Publishing - SSO Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Arc Publishing - SSO Domain and URLs single sign-on information](./media/arc-tutorial/tutorial_arc_url.png)

    1. <span data-ttu-id="7b659-154">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<Unique ID>`</span><span class="sxs-lookup"><span data-stu-id="7b659-154">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<Unique ID>`</span></span>

    1. <span data-ttu-id="7b659-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://arcpublishing-<Customer>.okta.com/sso/saml2/<Unique ID>`</span><span class="sxs-lookup"><span data-stu-id="7b659-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://arcpublishing-<Customer>.okta.com/sso/saml2/<Unique ID>`</span></span>

1. <span data-ttu-id="7b659-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7b659-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Arc Publishing - SSO Domain and URLs single sign-on information](./media/arc-tutorial/tutorial_arc_url1.png)

    <span data-ttu-id="7b659-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://arcpublishing-<Customer>.okta.com/sso/saml2/<Unique ID>`</span><span class="sxs-lookup"><span data-stu-id="7b659-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://arcpublishing-<Customer>.okta.com/sso/saml2/<Unique ID>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7b659-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7b659-159">These values are not real.</span></span> <span data-ttu-id="7b659-160">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="7b659-160">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7b659-161">Contact [Arc Publishing - SSO Client support team](mailto:inf@washpost.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7b659-161">Contact [Arc Publishing - SSO Client support team](mailto:inf@washpost.com) to get these values.</span></span> 

1. <span data-ttu-id="7b659-162">Arc Publishing - SSO application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="7b659-162">Arc Publishing - SSO application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7b659-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="7b659-163">Configure the following claims for this application.</span></span> <span data-ttu-id="7b659-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="7b659-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7b659-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="7b659-165">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/arc-tutorial/tutorial_arc_attribute.png)

1. <span data-ttu-id="7b659-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7b659-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="7b659-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="7b659-168">Attribute Name</span></span> | <span data-ttu-id="7b659-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="7b659-169">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="7b659-170">firstName</span><span class="sxs-lookup"><span data-stu-id="7b659-170">firstName</span></span> | <span data-ttu-id="7b659-171">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7b659-171">user.givenname</span></span> |
    | <span data-ttu-id="7b659-172">lastName</span><span class="sxs-lookup"><span data-stu-id="7b659-172">lastName</span></span> | <span data-ttu-id="7b659-173">user.surname</span><span class="sxs-lookup"><span data-stu-id="7b659-173">user.surname</span></span> |
    | <span data-ttu-id="7b659-174">email</span><span class="sxs-lookup"><span data-stu-id="7b659-174">email</span></span> | <span data-ttu-id="7b659-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="7b659-175">user.mail</span></span> |
    | <span data-ttu-id="7b659-176">groups</span><span class="sxs-lookup"><span data-stu-id="7b659-176">groups</span></span> | <span data-ttu-id="7b659-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="7b659-177">user.assignedroles</span></span> |

    1. <span data-ttu-id="7b659-178">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b659-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

     ![Configure Single Sign-On](./media/arc-tutorial/tutorial_attribute_04.png)

     ![Configure Single Sign-On](./media/arc-tutorial/tutorial_attribute_05.png)
    
    1. <span data-ttu-id="7b659-181">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7b659-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    1. <span data-ttu-id="7b659-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="7b659-182">From the **Value** list, type the attribute value shown for that row.</span></span>

    1. <span data-ttu-id="7b659-183">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="7b659-183">Leave the **Namespace** blank.</span></span>
    
    1. <span data-ttu-id="7b659-184">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="7b659-184">Click **Ok**</span></span>

    > [!NOTE]
    > <span data-ttu-id="7b659-185">Here the **groups** attribute is mapped with **user.assignedroles**.</span><span class="sxs-lookup"><span data-stu-id="7b659-185">Here the **groups** attribute is mapped with **user.assignedroles**.</span></span> <span data-ttu-id="7b659-186">These are custom roles created in Azure AD to map the group names back in application.</span><span class="sxs-lookup"><span data-stu-id="7b659-186">These are custom roles created in Azure AD to map the group names back in application.</span></span> <span data-ttu-id="7b659-187">You can find more guidance [here](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-app-role-management) on how to create custom roles in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b659-187">You can find more guidance [here](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-app-role-management) on how to create custom roles in Azure AD.</span></span> 

1. <span data-ttu-id="7b659-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7b659-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/arc-tutorial/tutorial_arc_certificate.png) 

1. <span data-ttu-id="7b659-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7b659-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/arc-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="7b659-192">On the **Arc Publishing - SSO Configuration** section, click **Configure Arc Publishing - SSO** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7b659-192">On the **Arc Publishing - SSO Configuration** section, click **Configure Arc Publishing - SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7b659-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7b659-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Arc Publishing - SSO Configuration](./media/arc-tutorial/tutorial_arc_configure.png) 

1. <span data-ttu-id="7b659-195">To configure single sign-on on **Arc Publishing - SSO** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Arc Publishing - SSO support team](mailto:inf@washpost.com).</span><span class="sxs-lookup"><span data-stu-id="7b659-195">To configure single sign-on on **Arc Publishing - SSO** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Arc Publishing - SSO support team](mailto:inf@washpost.com).</span></span> <span data-ttu-id="7b659-196">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7b659-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b659-197">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7b659-197">Create an Azure AD test user</span></span>

<span data-ttu-id="7b659-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b659-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7b659-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b659-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b659-201">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7b659-201">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/arc-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="7b659-203">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7b659-203">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/arc-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="7b659-205">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7b659-205">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/arc-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="7b659-207">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7b659-207">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/arc-tutorial/create_aaduser_04.png)

    1. <span data-ttu-id="7b659-209">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b659-209">In the **Name** box, type **BrittaSimon**.</span></span>

    1. <span data-ttu-id="7b659-210">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b659-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    1. <span data-ttu-id="7b659-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7b659-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    1. <span data-ttu-id="7b659-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b659-212">Click **Create**.</span></span>
 
### <a name="create-an-arc-publishing---sso-test-user"></a><span data-ttu-id="7b659-213">Create an Arc Publishing - SSO test user</span><span class="sxs-lookup"><span data-stu-id="7b659-213">Create an Arc Publishing - SSO test user</span></span>

<span data-ttu-id="7b659-214">The objective of this section is to create a user called Britta Simon in Arc Publishing - SSO.</span><span class="sxs-lookup"><span data-stu-id="7b659-214">The objective of this section is to create a user called Britta Simon in Arc Publishing - SSO.</span></span> <span data-ttu-id="7b659-215">Arc Publishing - SSO supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="7b659-215">Arc Publishing - SSO supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7b659-216">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7b659-216">There is no action item for you in this section.</span></span> <span data-ttu-id="7b659-217">A new user is created during an attempt to access Arc Publishing - SSO if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="7b659-217">A new user is created during an attempt to access Arc Publishing - SSO if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="7b659-218">If you need to create a user manually, contact [Arc Publishing - SSO support team](mailto:inf@washpost.com).</span><span class="sxs-lookup"><span data-stu-id="7b659-218">If you need to create a user manually, contact [Arc Publishing - SSO support team](mailto:inf@washpost.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7b659-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7b659-219">Assign the Azure AD test user</span></span>

<span data-ttu-id="7b659-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Arc Publishing - SSO.</span><span class="sxs-lookup"><span data-stu-id="7b659-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Arc Publishing - SSO.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7b659-222">**To assign Britta Simon to Arc Publishing - SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7b659-222">**To assign Britta Simon to Arc Publishing - SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="7b659-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7b659-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7b659-225">In the applications list, select **Arc Publishing - SSO**.</span><span class="sxs-lookup"><span data-stu-id="7b659-225">In the applications list, select **Arc Publishing - SSO**.</span></span>

    ![The Arc Publishing - SSO link in the Applications list](./media/arc-tutorial/tutorial_arc_app.png)  

1. <span data-ttu-id="7b659-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7b659-227">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="7b659-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7b659-229">Click **Add** button.</span></span> <span data-ttu-id="7b659-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b659-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="7b659-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7b659-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7b659-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b659-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7b659-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7b659-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b659-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7b659-235">Test single sign-on</span></span>

<span data-ttu-id="7b659-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7b659-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7b659-237">When you click the Arc Publishing - SSO tile in the Access Panel, you should get automatically signed-on to your Arc Publishing - SSO application.</span><span class="sxs-lookup"><span data-stu-id="7b659-237">When you click the Arc Publishing - SSO tile in the Access Panel, you should get automatically signed-on to your Arc Publishing - SSO application.</span></span>
<span data-ttu-id="7b659-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b659-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b659-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7b659-239">Additional resources</span></span>

* [<span data-ttu-id="7b659-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b659-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7b659-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b659-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/arc-tutorial/tutorial_general_01.png
[2]: ./media/arc-tutorial/tutorial_general_02.png
[3]: ./media/arc-tutorial/tutorial_general_03.png
[4]: ./media/arc-tutorial/tutorial_general_04.png

[100]: ./media/arc-tutorial/tutorial_general_100.png

[200]: ./media/arc-tutorial/tutorial_general_200.png
[201]: ./media/arc-tutorial/tutorial_general_201.png
[202]: ./media/arc-tutorial/tutorial_general_202.png
[203]: ./media/arc-tutorial/tutorial_general_203.png
