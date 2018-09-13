---
title: 'Tutorial: Azure Active Directory integration with Pega Systems | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pega Systems.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 31acf80f-1f4b-41f1-956f-a9fbae77ee69
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2017
ms.author: jeedes
ms.openlocfilehash: 224120f01cf6e1a32c85d1f50c6e3a30f50d243a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856104"
---
# <a name="tutorial-azure-active-directory-integration-with-pega-systems"></a><span data-ttu-id="ee80f-103">Tutorial: Azure Active Directory integration with Pega Systems</span><span class="sxs-lookup"><span data-stu-id="ee80f-103">Tutorial: Azure Active Directory integration with Pega Systems</span></span>

<span data-ttu-id="ee80f-104">In this tutorial, you learn how to integrate Pega Systems with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee80f-104">In this tutorial, you learn how to integrate Pega Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee80f-105">Integrating Pega Systems with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ee80f-105">Integrating Pega Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ee80f-106">You can control in Azure AD who has access to Pega Systems.</span><span class="sxs-lookup"><span data-stu-id="ee80f-106">You can control in Azure AD who has access to Pega Systems.</span></span>
- <span data-ttu-id="ee80f-107">You can enable your users to automatically get signed-on to Pega Systems (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ee80f-107">You can enable your users to automatically get signed-on to Pega Systems (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ee80f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee80f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ee80f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ee80f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee80f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee80f-110">Prerequisites</span></span>

<span data-ttu-id="ee80f-111">To configure Azure AD integration with Pega Systems, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ee80f-111">To configure Azure AD integration with Pega Systems, you need the following items:</span></span>

- <span data-ttu-id="ee80f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ee80f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee80f-113">A Pega Systems single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ee80f-113">A Pega Systems single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee80f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ee80f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee80f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ee80f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee80f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ee80f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee80f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee80f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee80f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ee80f-118">Scenario description</span></span>
<span data-ttu-id="ee80f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ee80f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee80f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ee80f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee80f-121">Adding Pega Systems from the gallery</span><span class="sxs-lookup"><span data-stu-id="ee80f-121">Adding Pega Systems from the gallery</span></span>
1. <span data-ttu-id="ee80f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ee80f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pega-systems-from-the-gallery"></a><span data-ttu-id="ee80f-123">Adding Pega Systems from the gallery</span><span class="sxs-lookup"><span data-stu-id="ee80f-123">Adding Pega Systems from the gallery</span></span>
<span data-ttu-id="ee80f-124">To configure the integration of Pega Systems into Azure AD, you need to add Pega Systems from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ee80f-124">To configure the integration of Pega Systems into Azure AD, you need to add Pega Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ee80f-125">**To add Pega Systems from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ee80f-125">**To add Pega Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ee80f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ee80f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="ee80f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ee80f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="ee80f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ee80f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="ee80f-133">In the search box, type **Pega Systems**, select **Pega Systems** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ee80f-133">In the search box, type **Pega Systems**, select **Pega Systems** from result panel then click **Add** button to add the application.</span></span>

    ![Pega Systems in the results list](./media/pegasystems-tutorial/tutorial_pegasystems_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ee80f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ee80f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ee80f-136">In this section, you configure and test Azure AD single sign-on with Pega Systems based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ee80f-136">In this section, you configure and test Azure AD single sign-on with Pega Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ee80f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pega Systems is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee80f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pega Systems is to a user in Azure AD.</span></span> <span data-ttu-id="ee80f-138">In other words, a link relationship between an Azure AD user and the related user in Pega Systems needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ee80f-138">In other words, a link relationship between an Azure AD user and the related user in Pega Systems needs to be established.</span></span>

<span data-ttu-id="ee80f-139">In Pega Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ee80f-139">In Pega Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ee80f-140">To configure and test Azure AD single sign-on with Pega Systems, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ee80f-140">To configure and test Azure AD single sign-on with Pega Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ee80f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ee80f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ee80f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee80f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ee80f-143">**[Create a Pega Systems test user](#create-a-pega-systems-test-user)** - to have a counterpart of Britta Simon in Pega Systems that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ee80f-143">**[Create a Pega Systems test user](#create-a-pega-systems-test-user)** - to have a counterpart of Britta Simon in Pega Systems that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ee80f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ee80f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ee80f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ee80f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ee80f-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ee80f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ee80f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pega Systems application.</span><span class="sxs-lookup"><span data-stu-id="ee80f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pega Systems application.</span></span>

<span data-ttu-id="ee80f-148">**To configure Azure AD single sign-on with Pega Systems, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ee80f-148">**To configure Azure AD single sign-on with Pega Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="ee80f-149">In the Azure portal, on the **Pega Systems** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-149">In the Azure portal, on the **Pega Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="ee80f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ee80f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/pegasystems-tutorial/tutorial_pegasystems_samlbase.png)

1. <span data-ttu-id="ee80f-153">On the **Pega Systems Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ee80f-153">On the **Pega Systems Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Pega Systems Domain and URLs single sign-on information](./media/pegasystems-tutorial/tutorial_pegasystems_url.png)

    <span data-ttu-id="ee80f-155">a.</span><span class="sxs-lookup"><span data-stu-id="ee80f-155">a.</span></span> <span data-ttu-id="ee80f-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io:443/prweb/sp/<INSTANCEID>`</span><span class="sxs-lookup"><span data-stu-id="ee80f-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io:443/prweb/sp/<INSTANCEID>`</span></span>

    <span data-ttu-id="ee80f-157">b.</span><span class="sxs-lookup"><span data-stu-id="ee80f-157">b.</span></span> <span data-ttu-id="ee80f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io:443/prweb/PRRestService/WebSSO/SAML/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="ee80f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io:443/prweb/PRRestService/WebSSO/SAML/AssertionConsumerService`</span></span>

1. <span data-ttu-id="ee80f-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ee80f-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Pega Systems Domain and URLs single sign-on information](./media/pegasystems-tutorial/tutorial_pegasystems_url1.png)

    <span data-ttu-id="ee80f-161">In the **Relay State** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io/prweb/sso`</span><span class="sxs-lookup"><span data-stu-id="ee80f-161">In the **Relay State** textbox, type a URL using the following pattern: `https://<CUSTOMERNAME>.pegacloud.io/prweb/sso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ee80f-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ee80f-162">These values are not real.</span></span> <span data-ttu-id="ee80f-163">Update these values with the actual Identifier, Reply URL, and Relay State URL.</span><span class="sxs-lookup"><span data-stu-id="ee80f-163">Update these values with the actual Identifier, Reply URL, and Relay State URL.</span></span> <span data-ttu-id="ee80f-164">You can find the values of Identifier and Reply URL from Pega application which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee80f-164">You can find the values of Identifier and Reply URL from Pega application which is explained later in this tutorial.</span></span> <span data-ttu-id="ee80f-165">For Relay State, please contact [Pega Systems Client support team](https://www.pega.com/contact-us) to get the value.</span><span class="sxs-lookup"><span data-stu-id="ee80f-165">For Relay State, please contact [Pega Systems Client support team](https://www.pega.com/contact-us) to get the value.</span></span> 

1. <span data-ttu-id="ee80f-166">The Pega Systems application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="ee80f-166">The Pega Systems application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ee80f-167">These claims are customer specific and depends on your requirement.</span><span class="sxs-lookup"><span data-stu-id="ee80f-167">These claims are customer specific and depends on your requirement.</span></span> <span data-ttu-id="ee80f-168">Following optional claims are example only which you can configure for your application.</span><span class="sxs-lookup"><span data-stu-id="ee80f-168">Following optional claims are example only which you can configure for your application.</span></span> <span data-ttu-id="ee80f-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="ee80f-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configure Single Sign-On](./media/pegasystems-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="ee80f-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ee80f-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ee80f-172">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ee80f-172">Attribute Name</span></span> | <span data-ttu-id="ee80f-173">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ee80f-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ee80f-174">uid</span><span class="sxs-lookup"><span data-stu-id="ee80f-174">uid</span></span> | *********** |
    | <span data-ttu-id="ee80f-175">cn</span><span class="sxs-lookup"><span data-stu-id="ee80f-175">cn</span></span>  | *********** |
    | <span data-ttu-id="ee80f-176">mail</span><span class="sxs-lookup"><span data-stu-id="ee80f-176">mail</span></span> | *********** |
    | <span data-ttu-id="ee80f-177">accessgroup</span><span class="sxs-lookup"><span data-stu-id="ee80f-177">accessgroup</span></span> | *********** |
    | <span data-ttu-id="ee80f-178">organization</span><span class="sxs-lookup"><span data-stu-id="ee80f-178">organization</span></span> | *********** |
    | <span data-ttu-id="ee80f-179">orgdivision</span><span class="sxs-lookup"><span data-stu-id="ee80f-179">orgdivision</span></span> | *********** |
    | <span data-ttu-id="ee80f-180">orgunit</span><span class="sxs-lookup"><span data-stu-id="ee80f-180">orgunit</span></span> | *********** |
    | <span data-ttu-id="ee80f-181">workgroup</span><span class="sxs-lookup"><span data-stu-id="ee80f-181">workgroup</span></span> | *********** |
    | <span data-ttu-id="ee80f-182">Phone</span><span class="sxs-lookup"><span data-stu-id="ee80f-182">Phone</span></span> | *********** |

    > [!NOTE]
    > <span data-ttu-id="ee80f-183">These are customer specific values.</span><span class="sxs-lookup"><span data-stu-id="ee80f-183">These are customer specific values.</span></span> <span data-ttu-id="ee80f-184">Please provide your appropriate values.</span><span class="sxs-lookup"><span data-stu-id="ee80f-184">Please provide your appropriate values.</span></span>

    <span data-ttu-id="ee80f-185">a.</span><span class="sxs-lookup"><span data-stu-id="ee80f-185">a.</span></span> <span data-ttu-id="ee80f-186">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="ee80f-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/pegasystems-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/pegasystems-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ee80f-189">b.</span><span class="sxs-lookup"><span data-stu-id="ee80f-189">b.</span></span> <span data-ttu-id="ee80f-190">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ee80f-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ee80f-191">c.</span><span class="sxs-lookup"><span data-stu-id="ee80f-191">c.</span></span> <span data-ttu-id="ee80f-192">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ee80f-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ee80f-193">d.</span><span class="sxs-lookup"><span data-stu-id="ee80f-193">d.</span></span> <span data-ttu-id="ee80f-194">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-194">Click **Ok**.</span></span>

1. <span data-ttu-id="ee80f-195">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ee80f-195">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/pegasystems-tutorial/tutorial_pegasystems_certificate.png) 
1. <span data-ttu-id="ee80f-197">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ee80f-197">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="ee80f-199">To configure single sign-on on **Pega Systems** side, open the **Pega Portal** with admin account in another browser window.</span><span class="sxs-lookup"><span data-stu-id="ee80f-199">To configure single sign-on on **Pega Systems** side, open the **Pega Portal** with admin account in another browser window.</span></span>

1. <span data-ttu-id="ee80f-200">Select **Create** -> **SysAdmin** -> **Authentication Service**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-200">Select **Create** -> **SysAdmin** -> **Authentication Service**.</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_pegasystems_admin.png)
    
1. <span data-ttu-id="ee80f-202">Perform following actions on **Create Aauthentication Service** screen:</span><span class="sxs-lookup"><span data-stu-id="ee80f-202">Perform following actions on **Create Aauthentication Service** screen:</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_pegasystems_admin1.png)

    <span data-ttu-id="ee80f-204">a.</span><span class="sxs-lookup"><span data-stu-id="ee80f-204">a.</span></span> <span data-ttu-id="ee80f-205">Select **SAML 2.0** from Type</span><span class="sxs-lookup"><span data-stu-id="ee80f-205">Select **SAML 2.0** from Type</span></span>

    <span data-ttu-id="ee80f-206">b.</span><span class="sxs-lookup"><span data-stu-id="ee80f-206">b.</span></span> <span data-ttu-id="ee80f-207">In the **Name** textbox, enter any name e.g Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ee80f-207">In the **Name** textbox, enter any name e.g Azure AD SSO</span></span>

    <span data-ttu-id="ee80f-208">c.</span><span class="sxs-lookup"><span data-stu-id="ee80f-208">c.</span></span> <span data-ttu-id="ee80f-209">In the **Short Description** textbox, enter any description</span><span class="sxs-lookup"><span data-stu-id="ee80f-209">In the **Short Description** textbox, enter any description</span></span>  

    <span data-ttu-id="ee80f-210">d.</span><span class="sxs-lookup"><span data-stu-id="ee80f-210">d.</span></span> <span data-ttu-id="ee80f-211">Click on **Create and open**</span><span class="sxs-lookup"><span data-stu-id="ee80f-211">Click on **Create and open**</span></span> 
    
1. <span data-ttu-id="ee80f-212">In **Identity Provider (IdP) information** section, click on **Import IdP metadata** and browse the metadata file which you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee80f-212">In **Identity Provider (IdP) information** section, click on **Import IdP metadata** and browse the metadata file which you have downloaded from the Azure portal.</span></span> <span data-ttu-id="ee80f-213">Click **Submit** to load the metadata.</span><span class="sxs-lookup"><span data-stu-id="ee80f-213">Click **Submit** to load the metadata.</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_pegasystems_admin2.png)
    
1. <span data-ttu-id="ee80f-215">This will populate the IdP data as shown below.</span><span class="sxs-lookup"><span data-stu-id="ee80f-215">This will populate the IdP data as shown below.</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_pegasystems_admin3.png)
    
1. <span data-ttu-id="ee80f-217">Perform following actions on **Service Provider (SP) settings** section:</span><span class="sxs-lookup"><span data-stu-id="ee80f-217">Perform following actions on **Service Provider (SP) settings** section:</span></span>

    ![Configure Single Sign-On Save button](./media/pegasystems-tutorial/tutorial_pegasystems_admin4.png)

    <span data-ttu-id="ee80f-219">a.</span><span class="sxs-lookup"><span data-stu-id="ee80f-219">a.</span></span> <span data-ttu-id="ee80f-220">Copy the **Entity Identification** value and paste back in Azure Portal's **Identifier** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee80f-220">Copy the **Entity Identification** value and paste back in Azure Portal's **Identifier** textbox.</span></span>

    <span data-ttu-id="ee80f-221">b.</span><span class="sxs-lookup"><span data-stu-id="ee80f-221">b.</span></span>  <span data-ttu-id="ee80f-222">Copy the **Assertion Consumer Service (ACS) location** value and paste back in Azure Portal's **Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee80f-222">Copy the **Assertion Consumer Service (ACS) location** value and paste back in Azure Portal's **Reply URL** textbox.</span></span>

    <span data-ttu-id="ee80f-223">c.</span><span class="sxs-lookup"><span data-stu-id="ee80f-223">c.</span></span> <span data-ttu-id="ee80f-224">Select **Disable request signing**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-224">Select **Disable request signing**.</span></span>

1. <span data-ttu-id="ee80f-225">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="ee80f-225">Click **Save**</span></span>
    
> [!TIP]
> <span data-ttu-id="ee80f-226">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="ee80f-226">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ee80f-227">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="ee80f-227">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ee80f-228">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee80f-228">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ee80f-229">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ee80f-229">Create an Azure AD test user</span></span>

<span data-ttu-id="ee80f-230">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee80f-230">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ee80f-232">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ee80f-232">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ee80f-233">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ee80f-233">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/pegasystems-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="ee80f-235">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-235">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/pegasystems-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="ee80f-237">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ee80f-237">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/pegasystems-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="ee80f-239">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ee80f-239">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/pegasystems-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ee80f-241">a.</span><span class="sxs-lookup"><span data-stu-id="ee80f-241">a.</span></span> <span data-ttu-id="ee80f-242">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-242">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee80f-243">b.</span><span class="sxs-lookup"><span data-stu-id="ee80f-243">b.</span></span> <span data-ttu-id="ee80f-244">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee80f-244">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ee80f-245">c.</span><span class="sxs-lookup"><span data-stu-id="ee80f-245">c.</span></span> <span data-ttu-id="ee80f-246">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ee80f-246">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ee80f-247">d.</span><span class="sxs-lookup"><span data-stu-id="ee80f-247">d.</span></span> <span data-ttu-id="ee80f-248">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-248">Click **Create**.</span></span>
 
### <a name="create-a-pega-systems-test-user"></a><span data-ttu-id="ee80f-249">Create a Pega Systems test user</span><span class="sxs-lookup"><span data-stu-id="ee80f-249">Create a Pega Systems test user</span></span>

<span data-ttu-id="ee80f-250">The objective of this section is to create a user called Britta Simon in Pega Systems.</span><span class="sxs-lookup"><span data-stu-id="ee80f-250">The objective of this section is to create a user called Britta Simon in Pega Systems.</span></span> <span data-ttu-id="ee80f-251">Please work with [Pega Systems Client support team](https://www.pega.com/contact-us) to create users in Pega Sysyems.</span><span class="sxs-lookup"><span data-stu-id="ee80f-251">Please work with [Pega Systems Client support team](https://www.pega.com/contact-us) to create users in Pega Sysyems.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ee80f-252">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ee80f-252">Assign the Azure AD test user</span></span>

<span data-ttu-id="ee80f-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pega Systems.</span><span class="sxs-lookup"><span data-stu-id="ee80f-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pega Systems.</span></span>

![Assign the user role][200] 

<span data-ttu-id="ee80f-255">**To assign Britta Simon to Pega Systems, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ee80f-255">**To assign Britta Simon to Pega Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="ee80f-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ee80f-258">In the applications list, select **Pega Systems**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-258">In the applications list, select **Pega Systems**.</span></span>

    ![The Pega Systems link in the Applications list](./media/pegasystems-tutorial/tutorial_pegasystems_app.png)  

1. <span data-ttu-id="ee80f-260">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ee80f-260">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="ee80f-262">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ee80f-262">Click **Add** button.</span></span> <span data-ttu-id="ee80f-263">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ee80f-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="ee80f-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ee80f-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ee80f-266">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ee80f-266">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ee80f-267">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ee80f-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ee80f-268">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ee80f-268">Test single sign-on</span></span>

<span data-ttu-id="ee80f-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ee80f-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ee80f-270">When you click the Pega Systems tile in the Access Panel, you should get automatically signed-on to your Pega Systems application.</span><span class="sxs-lookup"><span data-stu-id="ee80f-270">When you click the Pega Systems tile in the Access Panel, you should get automatically signed-on to your Pega Systems application.</span></span>
<span data-ttu-id="ee80f-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee80f-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee80f-272">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ee80f-272">Additional resources</span></span>

* [<span data-ttu-id="ee80f-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee80f-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ee80f-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee80f-274">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/pegasystems-tutorial/tutorial_general_01.png
[2]: ./media/pegasystems-tutorial/tutorial_general_02.png
[3]: ./media/pegasystems-tutorial/tutorial_general_03.png
[4]: ./media/pegasystems-tutorial/tutorial_general_04.png

[100]: ./media/pegasystems-tutorial/tutorial_general_100.png

[200]: ./media/pegasystems-tutorial/tutorial_general_200.png
[201]: ./media/pegasystems-tutorial/tutorial_general_201.png
[202]: ./media/pegasystems-tutorial/tutorial_general_202.png
[203]: ./media/pegasystems-tutorial/tutorial_general_203.png

