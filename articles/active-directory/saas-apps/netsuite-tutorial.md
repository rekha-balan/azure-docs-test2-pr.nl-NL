---
title: 'Tutorial: Azure Active Directory integration with NetSuite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and NetSuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2018
ms.author: jeedes
ms.openlocfilehash: 511fdcf587d16a59ff2bb11dfc55504b2218a569
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867014"
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="4b332-103">Tutorial: Azure Active Directory integration with NetSuite</span><span class="sxs-lookup"><span data-stu-id="4b332-103">Tutorial: Azure Active Directory integration with NetSuite</span></span>

<span data-ttu-id="4b332-104">In this tutorial, you learn how to integrate NetSuite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b332-104">In this tutorial, you learn how to integrate NetSuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b332-105">Integrating NetSuite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4b332-105">Integrating NetSuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b332-106">You can control in Azure AD who has access to NetSuite</span><span class="sxs-lookup"><span data-stu-id="4b332-106">You can control in Azure AD who has access to NetSuite</span></span>
- <span data-ttu-id="4b332-107">You can enable your users to automatically get signed-on to NetSuite (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4b332-107">You can enable your users to automatically get signed-on to NetSuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b332-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4b332-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b332-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4b332-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b332-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b332-110">Prerequisites</span></span>

<span data-ttu-id="4b332-111">To configure Azure AD integration with NetSuite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4b332-111">To configure Azure AD integration with NetSuite, you need the following items:</span></span>

- <span data-ttu-id="4b332-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4b332-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b332-113">A NetSuite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4b332-113">A NetSuite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b332-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4b332-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b332-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4b332-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b332-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4b332-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b332-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b332-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b332-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4b332-118">Scenario description</span></span>
<span data-ttu-id="4b332-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4b332-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b332-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4b332-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b332-121">Adding NetSuite from the gallery</span><span class="sxs-lookup"><span data-stu-id="4b332-121">Adding NetSuite from the gallery</span></span>
1. <span data-ttu-id="4b332-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b332-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="4b332-123">Adding NetSuite from the gallery</span><span class="sxs-lookup"><span data-stu-id="4b332-123">Adding NetSuite from the gallery</span></span>
<span data-ttu-id="4b332-124">To configure the integration of NetSuite into Azure AD, you need to add NetSuite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4b332-124">To configure the integration of NetSuite into Azure AD, you need to add NetSuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b332-125">**To add NetSuite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b332-125">**To add NetSuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b332-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4b332-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4b332-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4b332-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b332-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4b332-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="4b332-131">Click **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4b332-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4b332-133">In the search box, type **NetSuite**, select **NetSuite** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4b332-133">In the search box, type **NetSuite**, select **NetSuite** from result panel then click **Add** button to add the application.</span></span>

    ![NetSuite in the results list](./media/netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b332-135">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b332-135">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b332-136">In this section, you configure and test Azure AD single sign-on with NetSuite based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4b332-136">In this section, you configure and test Azure AD single sign-on with NetSuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b332-137">For single sign-on to work, Azure AD needs to know what the counterpart user in NetSuite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b332-137">For single sign-on to work, Azure AD needs to know what the counterpart user in NetSuite is to a user in Azure AD.</span></span> <span data-ttu-id="4b332-138">In other words, a link relationship between an Azure AD user and the related user in NetSuite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4b332-138">In other words, a link relationship between an Azure AD user and the related user in NetSuite needs to be established.</span></span>

<span data-ttu-id="4b332-139">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-139">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in NetSuite.</span></span>

<span data-ttu-id="4b332-140">To configure and test Azure AD single sign-on with NetSuite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4b332-140">To configure and test Azure AD single sign-on with NetSuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b332-141">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4b332-141">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4b332-142">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b332-142">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4b332-143">**[Creating a NetSuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in NetSuite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4b332-143">**[Creating a NetSuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in NetSuite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4b332-144">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b332-144">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4b332-145">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4b332-145">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b332-146">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b332-146">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b332-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetSuite application.</span><span class="sxs-lookup"><span data-stu-id="4b332-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetSuite application.</span></span>

<span data-ttu-id="4b332-148">**To configure Azure AD single sign-on with NetSuite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b332-148">**To configure Azure AD single sign-on with NetSuite, perform the following steps:**</span></span>

1. <span data-ttu-id="4b332-149">In the Azure portal, on the **NetSuite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4b332-149">In the Azure portal, on the **NetSuite** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4b332-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b332-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_NetSuite_samlbase.png)

1. <span data-ttu-id="4b332-153">On the **NetSuite Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b332-153">On the **NetSuite Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_NetSuite_url.png)

    <span data-ttu-id="4b332-155">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="4b332-155">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    `https://<tenant-name>.NetSuite.com/saml2/acs`

    `https://<tenant-name>.na1.NetSuite.com/saml2/acs`

    `https://<tenant-name>.na2.NetSuite.com/saml2/acs`

    `https://<tenant-name>.sandbox.NetSuite.com/saml2/acs`

    `https://<tenant-name>.na1.sandbox.NetSuite.com/saml2/acs`

    `https://<tenant-name>.na2.sandbox.NetSuite.com/saml2/acs`
    
    > [!NOTE]
    > <span data-ttu-id="4b332-156">These are not real values.</span><span class="sxs-lookup"><span data-stu-id="4b332-156">These are not real values.</span></span> <span data-ttu-id="4b332-157">Update these values with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="4b332-157">Update these values with the actual Reply URL.</span></span> <span data-ttu-id="4b332-158">Contact [NetSuite support team](http://www.NetSuite.com/portal/services/support.shtml) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4b332-158">Contact [NetSuite support team](http://www.NetSuite.com/portal/services/support.shtml) to get these values.</span></span>

1. <span data-ttu-id="4b332-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4b332-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_NetSuite_certificate.png) 

1. <span data-ttu-id="4b332-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4b332-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4b332-163">On the **NetSuite Configuration** section, click **Configure NetSuite** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4b332-163">On the **NetSuite Configuration** section, click **Configure NetSuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b332-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4b332-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_NetSuite_configure.png)

1. <span data-ttu-id="4b332-166">Open a new tab in your browser, and sign into your NetSuite company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4b332-166">Open a new tab in your browser, and sign into your NetSuite company site as an administrator.</span></span>

1. <span data-ttu-id="4b332-167">In the toolbar at the top of the page, click **Setup**, then navigate to **Company** and click **Enable Features**.</span><span class="sxs-lookup"><span data-stu-id="4b332-167">In the toolbar at the top of the page, click **Setup**, then navigate to **Company** and click **Enable Features**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-setupsaml.png)

1. <span data-ttu-id="4b332-169">In the toolbar at the middle of the page, click **SuiteCloud**.</span><span class="sxs-lookup"><span data-stu-id="4b332-169">In the toolbar at the middle of the page, click **SuiteCloud**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-suitecloud.png)

1. <span data-ttu-id="4b332-171">Under **Manage Authentication** section, select **SAML SINGLE SIGN-ON** to enable the SAML SINGLE SIGN-ON option in NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-171">Under **Manage Authentication** section, select **SAML SINGLE SIGN-ON** to enable the SAML SINGLE SIGN-ON option in NetSuite.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-ticksaml.png)

1. <span data-ttu-id="4b332-173">In the toolbar at the top of the page, click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="4b332-173">In the toolbar at the top of the page, click **Setup**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-setup.png)

1. <span data-ttu-id="4b332-175">From the **SETUP TASKS** list, click **Integration**.</span><span class="sxs-lookup"><span data-stu-id="4b332-175">From the **SETUP TASKS** list, click **Integration**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-integration.png)

1. <span data-ttu-id="4b332-177">In the **MANAGE AUTHENTICATION** section, click **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4b332-177">In the **MANAGE AUTHENTICATION** section, click **SAML Single Sign-on**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-saml.png)

1. <span data-ttu-id="4b332-179">On the **SAML Setup** page, under **NetSuite Configuration** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b332-179">On the **SAML Setup** page, under **NetSuite Configuration** section perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="4b332-181">a.</span><span class="sxs-lookup"><span data-stu-id="4b332-181">a.</span></span> <span data-ttu-id="4b332-182">Select **PRIMARY AUTHENTICATION METHOD**.</span><span class="sxs-lookup"><span data-stu-id="4b332-182">Select **PRIMARY AUTHENTICATION METHOD**.</span></span>

    <span data-ttu-id="4b332-183">b.</span><span class="sxs-lookup"><span data-stu-id="4b332-183">b.</span></span> <span data-ttu-id="4b332-184">For the field labeled **SAMLV2 IDENTITY PROVIDER METADATA**, select **UPLOAD IDP METADATA FILE**.</span><span class="sxs-lookup"><span data-stu-id="4b332-184">For the field labeled **SAMLV2 IDENTITY PROVIDER METADATA**, select **UPLOAD IDP METADATA FILE**.</span></span> <span data-ttu-id="4b332-185">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4b332-185">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    <span data-ttu-id="4b332-186">c.</span><span class="sxs-lookup"><span data-stu-id="4b332-186">c.</span></span> <span data-ttu-id="4b332-187">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="4b332-187">Click **Submit**.</span></span>

1. <span data-ttu-id="4b332-188">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span><span class="sxs-lookup"><span data-stu-id="4b332-188">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-attributes.png)

1. <span data-ttu-id="4b332-190">For the **Attribute Name** field, type in `account`.</span><span class="sxs-lookup"><span data-stu-id="4b332-190">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="4b332-191">For the **Attribute Value** field, type in your NetSuite account ID.</span><span class="sxs-lookup"><span data-stu-id="4b332-191">For the **Attribute Value** field, type in your NetSuite account ID.</span></span> <span data-ttu-id="4b332-192">This value is constant and change with account.</span><span class="sxs-lookup"><span data-stu-id="4b332-192">This value is constant and change with account.</span></span> <span data-ttu-id="4b332-193">Instructions on how to find your account ID are included below:</span><span class="sxs-lookup"><span data-stu-id="4b332-193">Instructions on how to find your account ID are included below:</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="4b332-195">a.</span><span class="sxs-lookup"><span data-stu-id="4b332-195">a.</span></span> <span data-ttu-id="4b332-196">In NetSuite, click **Setup** then navigate to **Company** and click **Company Information** from the top navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4b332-196">In NetSuite, click **Setup** then navigate to **Company** and click **Company Information** from the top navigation menu.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-com.png)

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-account-id.png)

    <span data-ttu-id="4b332-199">b.</span><span class="sxs-lookup"><span data-stu-id="4b332-199">b.</span></span> <span data-ttu-id="4b332-200">In the **Company Information** Page on the right column copy the **ACCOUNT ID**.</span><span class="sxs-lookup"><span data-stu-id="4b332-200">In the **Company Information** Page on the right column copy the **ACCOUNT ID**.</span></span>

    <span data-ttu-id="4b332-201">c.</span><span class="sxs-lookup"><span data-stu-id="4b332-201">c.</span></span> <span data-ttu-id="4b332-202">Paste the **Account ID** which you have copied from NetSuite account it into the **Attribute Value** field in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b332-202">Paste the **Account ID** which you have copied from NetSuite account it into the **Attribute Value** field in Azure AD.</span></span> 

1. <span data-ttu-id="4b332-203">Before users can perform single sign-on into NetSuite, they must first be assigned the appropriate permissions in NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-203">Before users can perform single sign-on into NetSuite, they must first be assigned the appropriate permissions in NetSuite.</span></span> <span data-ttu-id="4b332-204">Follow the instructions below to assign these permissions.</span><span class="sxs-lookup"><span data-stu-id="4b332-204">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="4b332-205">a.</span><span class="sxs-lookup"><span data-stu-id="4b332-205">a.</span></span> <span data-ttu-id="4b332-206">On the top navigation menu, click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="4b332-206">On the top navigation menu, click **Setup**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-setup.png)

    <span data-ttu-id="4b332-208">b.</span><span class="sxs-lookup"><span data-stu-id="4b332-208">b.</span></span> <span data-ttu-id="4b332-209">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span><span class="sxs-lookup"><span data-stu-id="4b332-209">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="4b332-211">c.</span><span class="sxs-lookup"><span data-stu-id="4b332-211">c.</span></span> <span data-ttu-id="4b332-212">Click **New Role**.</span><span class="sxs-lookup"><span data-stu-id="4b332-212">Click **New Role**.</span></span>

    <span data-ttu-id="4b332-213">d.</span><span class="sxs-lookup"><span data-stu-id="4b332-213">d.</span></span> <span data-ttu-id="4b332-214">Type in a **Name** for your new role.</span><span class="sxs-lookup"><span data-stu-id="4b332-214">Type in a **Name** for your new role.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-new-role.png)

    <span data-ttu-id="4b332-216">e.</span><span class="sxs-lookup"><span data-stu-id="4b332-216">e.</span></span> <span data-ttu-id="4b332-217">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4b332-217">Click **Save**.</span></span>

    <span data-ttu-id="4b332-218">f.</span><span class="sxs-lookup"><span data-stu-id="4b332-218">f.</span></span> <span data-ttu-id="4b332-219">In the menu on the top, click **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="4b332-219">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="4b332-220">Then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="4b332-220">Then click **Setup**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-sso.png)

    <span data-ttu-id="4b332-222">g.</span><span class="sxs-lookup"><span data-stu-id="4b332-222">g.</span></span> <span data-ttu-id="4b332-223">Select **SAML Single Sign-on**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4b332-223">Select **SAML Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="4b332-224">h.</span><span class="sxs-lookup"><span data-stu-id="4b332-224">h.</span></span> <span data-ttu-id="4b332-225">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4b332-225">Click **Save**.</span></span>

    <span data-ttu-id="4b332-226">i.</span><span class="sxs-lookup"><span data-stu-id="4b332-226">i.</span></span> <span data-ttu-id="4b332-227">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="4b332-227">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-setup.png)

    <span data-ttu-id="4b332-229">j.</span><span class="sxs-lookup"><span data-stu-id="4b332-229">j.</span></span> <span data-ttu-id="4b332-230">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="4b332-230">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="4b332-232">k.</span><span class="sxs-lookup"><span data-stu-id="4b332-232">k.</span></span> <span data-ttu-id="4b332-233">Select a test user.</span><span class="sxs-lookup"><span data-stu-id="4b332-233">Select a test user.</span></span> <span data-ttu-id="4b332-234">Then click **Edit** and then navigate to **Access** tab.</span><span class="sxs-lookup"><span data-stu-id="4b332-234">Then click **Edit** and then navigate to **Access** tab.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="4b332-236">l.</span><span class="sxs-lookup"><span data-stu-id="4b332-236">l.</span></span> <span data-ttu-id="4b332-237">On the Roles dialog, assign the appropriate role that you have created.</span><span class="sxs-lookup"><span data-stu-id="4b332-237">On the Roles dialog, assign the appropriate role that you have created.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/ns-add-role.png)

    <span data-ttu-id="4b332-239">m.</span><span class="sxs-lookup"><span data-stu-id="4b332-239">m.</span></span> <span data-ttu-id="4b332-240">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4b332-240">Click **Save**.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b332-241">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4b332-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b332-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b332-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4b332-244">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b332-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b332-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4b332-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/NetSuite-tutorial/create_aaduser_01.png) 

1.  <span data-ttu-id="4b332-247">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4b332-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/NetSuite-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4b332-249">At the top of the dialog, click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b332-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/NetSuite-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4b332-251">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b332-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/NetSuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b332-253">a.</span><span class="sxs-lookup"><span data-stu-id="4b332-253">a.</span></span> <span data-ttu-id="4b332-254">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b332-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b332-255">b.</span><span class="sxs-lookup"><span data-stu-id="4b332-255">b.</span></span> <span data-ttu-id="4b332-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b332-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b332-257">c.</span><span class="sxs-lookup"><span data-stu-id="4b332-257">c.</span></span> <span data-ttu-id="4b332-258">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4b332-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b332-259">d.</span><span class="sxs-lookup"><span data-stu-id="4b332-259">d.</span></span> <span data-ttu-id="4b332-260">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b332-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="4b332-261">Creating a NetSuite test user</span><span class="sxs-lookup"><span data-stu-id="4b332-261">Creating a NetSuite test user</span></span>

<span data-ttu-id="4b332-262">In this section, a user called Britta Simon is created in NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-262">In this section, a user called Britta Simon is created in NetSuite.</span></span> <span data-ttu-id="4b332-263">NetSuite supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="4b332-263">NetSuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="4b332-264">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="4b332-264">There is no action item for you in this section.</span></span> <span data-ttu-id="4b332-265">If a user doesn't already exist in NetSuite, a new one is created when you attempt to access NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-265">If a user doesn't already exist in NetSuite, a new one is created when you attempt to access NetSuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b332-266">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4b332-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b332-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetSuite.</span><span class="sxs-lookup"><span data-stu-id="4b332-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetSuite.</span></span>

![Assign User][200] 

<span data-ttu-id="4b332-269">**To assign Britta Simon to NetSuite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4b332-269">**To assign Britta Simon to NetSuite, perform the following steps:**</span></span>

1. <span data-ttu-id="4b332-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4b332-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4b332-272">In the applications list, select **NetSuite**.</span><span class="sxs-lookup"><span data-stu-id="4b332-272">In the applications list, select **NetSuite**.</span></span>

    ![Configure Single Sign-On](./media/NetSuite-tutorial/tutorial_NetSuite_app.png) 

1. <span data-ttu-id="4b332-274">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4b332-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4b332-276">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4b332-276">Click **Add** button.</span></span> <span data-ttu-id="4b332-277">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b332-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4b332-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4b332-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4b332-280">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b332-280">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4b332-281">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4b332-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b332-282">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4b332-282">Testing single sign-on</span></span>

<span data-ttu-id="4b332-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4b332-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b332-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **NetSuite**.</span><span class="sxs-lookup"><span data-stu-id="4b332-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **NetSuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b332-285">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4b332-285">Additional resources</span></span>

* [<span data-ttu-id="4b332-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b332-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4b332-287">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b332-287">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="4b332-288">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="4b332-288">Configure User Provisioning</span></span>](NetSuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/NetSuite-tutorial/tutorial_general_01.png
[2]: ./media/NetSuite-tutorial/tutorial_general_02.png
[3]: ./media/NetSuite-tutorial/tutorial_general_03.png
[4]: ./media/NetSuite-tutorial/tutorial_general_04.png

[100]: ./media/NetSuite-tutorial/tutorial_general_100.png

[200]: ./media/NetSuite-tutorial/tutorial_general_200.png
[201]: ./media/NetSuite-tutorial/tutorial_general_201.png
[202]: ./media/NetSuite-tutorial/tutorial_general_202.png
[203]: ./media/NetSuite-tutorial/tutorial_general_203.png

