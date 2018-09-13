---
title: 'Tutorial: Azure Active Directory integration with OrgChart Now | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OrgChart Now.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 50a1522f-81de-4d14-9b6b-dd27bb1338a4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2018
ms.author: jeedes
ms.openlocfilehash: e23d76074f4b428b672e0cd5aeeaba99d080a4cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865163"
---
# <a name="tutorial-azure-active-directory-integration-with-orgchart-now"></a><span data-ttu-id="39b1f-103">Tutorial: Azure Active Directory integration with OrgChart Now</span><span class="sxs-lookup"><span data-stu-id="39b1f-103">Tutorial: Azure Active Directory integration with OrgChart Now</span></span>

<span data-ttu-id="39b1f-104">In this tutorial, you learn how to integrate OrgChart Now with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39b1f-104">In this tutorial, you learn how to integrate OrgChart Now with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39b1f-105">Integrating OrgChart Now with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="39b1f-105">Integrating OrgChart Now with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="39b1f-106">You can control in Azure AD who has access to OrgChart Now.</span><span class="sxs-lookup"><span data-stu-id="39b1f-106">You can control in Azure AD who has access to OrgChart Now.</span></span>
- <span data-ttu-id="39b1f-107">You can enable your users to automatically get signed-on to OrgChart Now (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="39b1f-107">You can enable your users to automatically get signed-on to OrgChart Now (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="39b1f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="39b1f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="39b1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="39b1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39b1f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39b1f-110">Prerequisites</span></span>

<span data-ttu-id="39b1f-111">To configure Azure AD integration with OrgChart Now, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="39b1f-111">To configure Azure AD integration with OrgChart Now, you need the following items:</span></span>

- <span data-ttu-id="39b1f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="39b1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39b1f-113">An OrgChart Now single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="39b1f-113">An OrgChart Now single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39b1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="39b1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39b1f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="39b1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39b1f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="39b1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39b1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39b1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39b1f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="39b1f-118">Scenario description</span></span>
<span data-ttu-id="39b1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="39b1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39b1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="39b1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39b1f-121">Adding OrgChart Now from the gallery</span><span class="sxs-lookup"><span data-stu-id="39b1f-121">Adding OrgChart Now from the gallery</span></span>
1. <span data-ttu-id="39b1f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39b1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-orgchart-now-from-the-gallery"></a><span data-ttu-id="39b1f-123">Adding OrgChart Now from the gallery</span><span class="sxs-lookup"><span data-stu-id="39b1f-123">Adding OrgChart Now from the gallery</span></span>
<span data-ttu-id="39b1f-124">To configure the integration of OrgChart Now into Azure AD, you need to add OrgChart Now from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="39b1f-124">To configure the integration of OrgChart Now into Azure AD, you need to add OrgChart Now from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39b1f-125">**To add OrgChart Now from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39b1f-125">**To add OrgChart Now from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="39b1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="39b1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="39b1f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="39b1f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="39b1f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="39b1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="39b1f-133">In the search box, type **OrgChart Now**, select **OrgChart Now** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="39b1f-133">In the search box, type **OrgChart Now**, select **OrgChart Now** from result panel then click **Add** button to add the application.</span></span>

    ![OrgChart Now in the results list](./media/orgchartnow-tutorial/tutorial_orgchartnow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="39b1f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39b1f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="39b1f-136">In this section, you configure and test Azure AD single sign-on with OrgChart Now based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39b1f-136">In this section, you configure and test Azure AD single sign-on with OrgChart Now based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39b1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OrgChart Now is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39b1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OrgChart Now is to a user in Azure AD.</span></span> <span data-ttu-id="39b1f-138">In other words, a link relationship between an Azure AD user and the related user in OrgChart Now needs to be established.</span><span class="sxs-lookup"><span data-stu-id="39b1f-138">In other words, a link relationship between an Azure AD user and the related user in OrgChart Now needs to be established.</span></span>

<span data-ttu-id="39b1f-139">To configure and test Azure AD single sign-on with OrgChart Now, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="39b1f-139">To configure and test Azure AD single sign-on with OrgChart Now, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="39b1f-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="39b1f-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="39b1f-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39b1f-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="39b1f-142">**[Create an OrgChart Now test user](#create-an-orgchart-now-test-user)** - to have a counterpart of Britta Simon in OrgChart Now that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="39b1f-142">**[Create an OrgChart Now test user](#create-an-orgchart-now-test-user)** - to have a counterpart of Britta Simon in OrgChart Now that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="39b1f-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="39b1f-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="39b1f-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="39b1f-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="39b1f-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="39b1f-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="39b1f-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OrgChart Now application.</span><span class="sxs-lookup"><span data-stu-id="39b1f-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OrgChart Now application.</span></span>

<span data-ttu-id="39b1f-147">**To configure Azure AD single sign-on with OrgChart Now, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39b1f-147">**To configure Azure AD single sign-on with OrgChart Now, perform the following steps:**</span></span>

1. <span data-ttu-id="39b1f-148">In the Azure portal, on the **OrgChart Now** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-148">In the Azure portal, on the **OrgChart Now** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="39b1f-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="39b1f-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/orgchartnow-tutorial/tutorial_orgchartnow_samlbase.png)

1. <span data-ttu-id="39b1f-152">On the **OrgChart Now Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="39b1f-152">On the **OrgChart Now Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![OrgChart Now Domain and URLs single sign-on information](./media/orgchartnow-tutorial/tutorial_orgchartnow_url.png)

    <span data-ttu-id="39b1f-154">In the **Identifier** textbox, type a URL: `https://sso2.orgchartnow.com`</span><span class="sxs-lookup"><span data-stu-id="39b1f-154">In the **Identifier** textbox, type a URL: `https://sso2.orgchartnow.com`</span></span>

1. <span data-ttu-id="39b1f-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="39b1f-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![OrgChart Now Domain and URLs single sign-on information](./media/orgchartnow-tutorial/tutorial_orgchartnow_url1.png)

    <span data-ttu-id="39b1f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso2.orgchartnow.com/Shibboleth.sso/Login?entityID=<YourEntityID>&target=https://sso2.orgchartnow.com`</span><span class="sxs-lookup"><span data-stu-id="39b1f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso2.orgchartnow.com/Shibboleth.sso/Login?entityID=<YourEntityID>&target=https://sso2.orgchartnow.com`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="39b1f-158">`<YourEntityID>` is the SAML Entity ID copied from the Quick Reference section, described later in tutorial.</span><span class="sxs-lookup"><span data-stu-id="39b1f-158">`<YourEntityID>` is the SAML Entity ID copied from the Quick Reference section, described later in tutorial.</span></span>

1. <span data-ttu-id="39b1f-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="39b1f-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/orgchartnow-tutorial/tutorial_orgchartnow_certificate.png) 

1. <span data-ttu-id="39b1f-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="39b1f-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/orgchartnow-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="39b1f-163">On the **OrgChart Now Configuration** section, click **Configure OrgChart Now** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="39b1f-163">On the **OrgChart Now Configuration** section, click **Configure OrgChart Now** to open **Configure sign-on** window.</span></span> <span data-ttu-id="39b1f-164">Copy the **SAML Entity ID** from the **Quick Reference section** and use it to complete **Sign-on URL** in **OrgChart Now Domain and URLs section**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-164">Copy the **SAML Entity ID** from the **Quick Reference section** and use it to complete **Sign-on URL** in **OrgChart Now Domain and URLs section**.</span></span>

    ![OrgChart Now Configuration](./media/orgchartnow-tutorial/tutorial_orgchartnow_configure.png) 

1. <span data-ttu-id="39b1f-166">To configure single sign-on on **OrgChart Now** side, you need to send the downloaded **Metadata XML** to [OrgChart Now support team](mailto:ocnsupport@officeworksoftware.com).</span><span class="sxs-lookup"><span data-stu-id="39b1f-166">To configure single sign-on on **OrgChart Now** side, you need to send the downloaded **Metadata XML** to [OrgChart Now support team](mailto:ocnsupport@officeworksoftware.com).</span></span> <span data-ttu-id="39b1f-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="39b1f-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="39b1f-168">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39b1f-168">Create an Azure AD test user</span></span>

<span data-ttu-id="39b1f-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39b1f-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="39b1f-171">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39b1f-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="39b1f-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="39b1f-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/orgchartnow-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="39b1f-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/orgchartnow-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="39b1f-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="39b1f-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/orgchartnow-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="39b1f-178">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39b1f-178">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/orgchartnow-tutorial/create_aaduser_04.png)

    <span data-ttu-id="39b1f-180">a.</span><span class="sxs-lookup"><span data-stu-id="39b1f-180">a.</span></span> <span data-ttu-id="39b1f-181">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39b1f-182">b.</span><span class="sxs-lookup"><span data-stu-id="39b1f-182">b.</span></span> <span data-ttu-id="39b1f-183">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39b1f-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="39b1f-184">c.</span><span class="sxs-lookup"><span data-stu-id="39b1f-184">c.</span></span> <span data-ttu-id="39b1f-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="39b1f-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="39b1f-186">d.</span><span class="sxs-lookup"><span data-stu-id="39b1f-186">d.</span></span> <span data-ttu-id="39b1f-187">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-187">Click **Create**.</span></span>
 
### <a name="create-an-orgchart-now-test-user"></a><span data-ttu-id="39b1f-188">Create an OrgChart Now test user</span><span class="sxs-lookup"><span data-stu-id="39b1f-188">Create an OrgChart Now test user</span></span>

<span data-ttu-id="39b1f-189">To enable Azure AD users to log in to OrgChart Now, they must be provisioned into OrgChart Now.</span><span class="sxs-lookup"><span data-stu-id="39b1f-189">To enable Azure AD users to log in to OrgChart Now, they must be provisioned into OrgChart Now.</span></span> 

1. <span data-ttu-id="39b1f-190">OrgChart Now supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="39b1f-190">OrgChart Now supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="39b1f-191">A new user is created during an attempt to access OrgChart Now if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="39b1f-191">A new user is created during an attempt to access OrgChart Now if it doesn't exist yet.</span></span> <span data-ttu-id="39b1f-192">The just-in-time user provisioning feature will only create a **read-only** user when an SSO request comes from a recognized IDP and the email in the SAML assertion is not found in the user list.</span><span class="sxs-lookup"><span data-stu-id="39b1f-192">The just-in-time user provisioning feature will only create a **read-only** user when an SSO request comes from a recognized IDP and the email in the SAML assertion is not found in the user list.</span></span> <span data-ttu-id="39b1f-193">For this auto provisioning feature you need to create an access group titled **General** in OrgChart Now.</span><span class="sxs-lookup"><span data-stu-id="39b1f-193">For this auto provisioning feature you need to create an access group titled **General** in OrgChart Now.</span></span> <span data-ttu-id="39b1f-194">Please follow the below steps to create an access group:</span><span class="sxs-lookup"><span data-stu-id="39b1f-194">Please follow the below steps to create an access group:</span></span>

    <span data-ttu-id="39b1f-195">a.</span><span class="sxs-lookup"><span data-stu-id="39b1f-195">a.</span></span> <span data-ttu-id="39b1f-196">Go to the **Manage Groups** option after clicking the **gear** in the top right corner of the UI.</span><span class="sxs-lookup"><span data-stu-id="39b1f-196">Go to the **Manage Groups** option after clicking the **gear** in the top right corner of the UI.</span></span>

    ![OrgChart Now groups](./media/orgchartnow-tutorial/tutorial_orgchartnow_manage.png)    

    <span data-ttu-id="39b1f-198">b.</span><span class="sxs-lookup"><span data-stu-id="39b1f-198">b.</span></span> <span data-ttu-id="39b1f-199">Select the **Add** icon and name the group **General** then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-199">Select the **Add** icon and name the group **General** then click **OK**.</span></span> 

    ![OrgChart Now add](./media/orgchartnow-tutorial/tutorial_orgchartnow_add.png)

    <span data-ttu-id="39b1f-201">c.</span><span class="sxs-lookup"><span data-stu-id="39b1f-201">c.</span></span> <span data-ttu-id="39b1f-202">Select the folder(s) you wish the general or read-only users to be able to access:</span><span class="sxs-lookup"><span data-stu-id="39b1f-202">Select the folder(s) you wish the general or read-only users to be able to access:</span></span>

    ![OrgChart Now folders](./media/orgchartnow-tutorial/tutorial_orgchartnow_chart.png)

    <span data-ttu-id="39b1f-204">d.</span><span class="sxs-lookup"><span data-stu-id="39b1f-204">d.</span></span> <span data-ttu-id="39b1f-205">**Lock** the folders so that only Admin users can modify them.</span><span class="sxs-lookup"><span data-stu-id="39b1f-205">**Lock** the folders so that only Admin users can modify them.</span></span> <span data-ttu-id="39b1f-206">Then press **OK**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-206">Then press **OK**.</span></span>

    ![OrgChart Now lock](./media/orgchartnow-tutorial/tutorial_orgchartnow_lock.png)

1. <span data-ttu-id="39b1f-208">To create **Admin** users and **read/write** users, you must manually create a user in order to get access to their privilege level via SSO.</span><span class="sxs-lookup"><span data-stu-id="39b1f-208">To create **Admin** users and **read/write** users, you must manually create a user in order to get access to their privilege level via SSO.</span></span> <span data-ttu-id="39b1f-209">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39b1f-209">To provision a user account, perform the following steps:</span></span>

    <span data-ttu-id="39b1f-210">a.</span><span class="sxs-lookup"><span data-stu-id="39b1f-210">a.</span></span> <span data-ttu-id="39b1f-211">Log in to OrgChart Now as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="39b1f-211">Log in to OrgChart Now as a Security Administrator.</span></span>

    <span data-ttu-id="39b1f-212">b.</span><span class="sxs-lookup"><span data-stu-id="39b1f-212">b.</span></span>  <span data-ttu-id="39b1f-213">Click on **Settings** on the top right corner and then navigate to **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-213">Click on **Settings** on the top right corner and then navigate to **Manage Users**.</span></span>

    ![OrgChart Now settings](./media/orgchartnow-tutorial/tutorial_orgchartnow_settings.png)

    <span data-ttu-id="39b1f-215">c.</span><span class="sxs-lookup"><span data-stu-id="39b1f-215">c.</span></span> <span data-ttu-id="39b1f-216">Click on **Add** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39b1f-216">Click on **Add** and perform the following steps:</span></span>

    ![OrgChart Now manage](./media/orgchartnow-tutorial/tutorial_orgchartnow_manageusers.png)

    * <span data-ttu-id="39b1f-218">In the **User ID** textbox, enter the User ID like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-218">In the **User ID** textbox, enter the User ID like **brittasimon@contoso.com**.</span></span>

    * <span data-ttu-id="39b1f-219">In **Email Address** text box, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-219">In **Email Address** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    * <span data-ttu-id="39b1f-220">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-220">Click **Add**.</span></span>
    
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="39b1f-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="39b1f-221">Assign the Azure AD test user</span></span>

<span data-ttu-id="39b1f-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OrgChart Now.</span><span class="sxs-lookup"><span data-stu-id="39b1f-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OrgChart Now.</span></span>

![Assign the user role][200] 

<span data-ttu-id="39b1f-224">**To assign Britta Simon to OrgChart Now, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39b1f-224">**To assign Britta Simon to OrgChart Now, perform the following steps:**</span></span>

1. <span data-ttu-id="39b1f-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="39b1f-227">In the applications list, select **OrgChart Now**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-227">In the applications list, select **OrgChart Now**.</span></span>

    ![The OrgChart Now link in the Applications list](./media/orgchartnow-tutorial/tutorial_orgchartnow_app.png)  

1. <span data-ttu-id="39b1f-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="39b1f-229">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="39b1f-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="39b1f-231">Click **Add** button.</span></span> <span data-ttu-id="39b1f-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39b1f-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="39b1f-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="39b1f-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="39b1f-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="39b1f-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="39b1f-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="39b1f-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="39b1f-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="39b1f-237">Test single sign-on</span></span>

<span data-ttu-id="39b1f-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="39b1f-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="39b1f-239">When you click the OrgChart Now tile in the Access Panel, you should get automatically signed-on to your OrgChart Now application.</span><span class="sxs-lookup"><span data-stu-id="39b1f-239">When you click the OrgChart Now tile in the Access Panel, you should get automatically signed-on to your OrgChart Now application.</span></span>
<span data-ttu-id="39b1f-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39b1f-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="39b1f-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="39b1f-241">Additional resources</span></span>

* [<span data-ttu-id="39b1f-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39b1f-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="39b1f-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39b1f-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/orgchartnow-tutorial/tutorial_general_01.png
[2]: ./media/orgchartnow-tutorial/tutorial_general_02.png
[3]: ./media/orgchartnow-tutorial/tutorial_general_03.png
[4]: ./media/orgchartnow-tutorial/tutorial_general_04.png

[100]: ./media/orgchartnow-tutorial/tutorial_general_100.png

[200]: ./media/orgchartnow-tutorial/tutorial_general_200.png
[201]: ./media/orgchartnow-tutorial/tutorial_general_201.png
[202]: ./media/orgchartnow-tutorial/tutorial_general_202.png
[203]: ./media/orgchartnow-tutorial/tutorial_general_203.png

