---
title: 'Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and MOVEit Transfer - Azure AD integration.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: e73ca95c27e7c9ef0799107dadc58c17aea5a9ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869356"
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="c7feb-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="c7feb-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="c7feb-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7feb-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7feb-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c7feb-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7feb-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c7feb-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="c7feb-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c7feb-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c7feb-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7feb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c7feb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c7feb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7feb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7feb-110">Prerequisites</span></span>

<span data-ttu-id="c7feb-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c7feb-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="c7feb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c7feb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7feb-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c7feb-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7feb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c7feb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7feb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c7feb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7feb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c7feb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7feb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7feb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7feb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c7feb-118">Scenario description</span></span>
<span data-ttu-id="c7feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c7feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7feb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c7feb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7feb-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span><span class="sxs-lookup"><span data-stu-id="c7feb-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
1. <span data-ttu-id="c7feb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c7feb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="c7feb-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span><span class="sxs-lookup"><span data-stu-id="c7feb-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="c7feb-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c7feb-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7feb-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c7feb-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7feb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c7feb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c7feb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7feb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c7feb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c7feb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c7feb-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c7feb-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer - Azure AD integration in the results list](./media/moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c7feb-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c7feb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c7feb-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7feb-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7feb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7feb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="c7feb-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c7feb-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="c7feb-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c7feb-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7feb-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c7feb-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7feb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c7feb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c7feb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7feb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c7feb-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c7feb-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c7feb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c7feb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c7feb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c7feb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c7feb-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c7feb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c7feb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span><span class="sxs-lookup"><span data-stu-id="c7feb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="c7feb-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c7feb-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="c7feb-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c7feb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c7feb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

1. <span data-ttu-id="c7feb-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c7feb-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="c7feb-155">a.</span><span class="sxs-lookup"><span data-stu-id="c7feb-155">a.</span></span> <span data-ttu-id="c7feb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="c7feb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="c7feb-157">b.</span><span class="sxs-lookup"><span data-stu-id="c7feb-157">b.</span></span> <span data-ttu-id="c7feb-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="c7feb-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="c7feb-159">c.</span><span class="sxs-lookup"><span data-stu-id="c7feb-159">c.</span></span> <span data-ttu-id="c7feb-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="c7feb-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="c7feb-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="c7feb-161">These values are not real.</span></span> <span data-ttu-id="c7feb-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="c7feb-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c7feb-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="c7feb-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

1. <span data-ttu-id="c7feb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c7feb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

1. <span data-ttu-id="c7feb-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c7feb-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/moveittransfer-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="c7feb-168">Sign on to your MOVEit Transfer tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c7feb-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

1. <span data-ttu-id="c7feb-169">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-169">On the left navigation pane, click **Settings**.</span></span>

    ![Settings Section On App side](./media/moveittransfer-tutorial/tutorial_moveittransfer_000.png)

1. <span data-ttu-id="c7feb-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Security Policies On App side](./media/moveittransfer-tutorial/tutorial_moveittransfer_001.png)

1. <span data-ttu-id="c7feb-173">Click the Metadata URL link to download the metadata document.</span><span class="sxs-lookup"><span data-stu-id="c7feb-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![Service Provider Metadata URL](./media/moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="c7feb-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span><span class="sxs-lookup"><span data-stu-id="c7feb-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="c7feb-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="c7feb-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configure Single Sign-On On App side](./media/moveittransfer-tutorial/tutorial_moveittransfer_007.png)

1. <span data-ttu-id="c7feb-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="c7feb-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Add Identity Provider](./media/moveittransfer-tutorial/tutorial_moveittransfer_003.png)

1. <span data-ttu-id="c7feb-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="c7feb-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![SAML Identity Provider](./media/moveittransfer-tutorial/tutorial_moveittransfer_004.png)

1. <span data-ttu-id="c7feb-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Federated Identity Provider Settings](./media/moveittransfer-tutorial/tutorial_moveittransfer_005.png)

1. <span data-ttu-id="c7feb-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="c7feb-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Edit Federated Identity Provider Settings](./media/moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="c7feb-186">a.</span><span class="sxs-lookup"><span data-stu-id="c7feb-186">a.</span></span> <span data-ttu-id="c7feb-187">Select **SAML NameID** as **Login name**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="c7feb-188">b.</span><span class="sxs-lookup"><span data-stu-id="c7feb-188">b.</span></span> <span data-ttu-id="c7feb-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="c7feb-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="c7feb-190">c.</span><span class="sxs-lookup"><span data-stu-id="c7feb-190">c.</span></span> <span data-ttu-id="c7feb-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="c7feb-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="c7feb-192">d.</span><span class="sxs-lookup"><span data-stu-id="c7feb-192">d.</span></span> <span data-ttu-id="c7feb-193">Select **Yes** as **Auto-create account on signon**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="c7feb-194">e.</span><span class="sxs-lookup"><span data-stu-id="c7feb-194">e.</span></span> <span data-ttu-id="c7feb-195">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c7feb-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c7feb-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c7feb-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7feb-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c7feb-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7feb-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7feb-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c7feb-199">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c7feb-199">Create an Azure AD test user</span></span>

<span data-ttu-id="c7feb-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7feb-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c7feb-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c7feb-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7feb-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c7feb-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/moveittransfer-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c7feb-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/moveittransfer-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c7feb-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c7feb-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/moveittransfer-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c7feb-209">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c7feb-209">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c7feb-211">a.</span><span class="sxs-lookup"><span data-stu-id="c7feb-211">a.</span></span> <span data-ttu-id="c7feb-212">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7feb-213">b.</span><span class="sxs-lookup"><span data-stu-id="c7feb-213">b.</span></span> <span data-ttu-id="c7feb-214">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7feb-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c7feb-215">c.</span><span class="sxs-lookup"><span data-stu-id="c7feb-215">c.</span></span> <span data-ttu-id="c7feb-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c7feb-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c7feb-217">d.</span><span class="sxs-lookup"><span data-stu-id="c7feb-217">d.</span></span> <span data-ttu-id="c7feb-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="c7feb-219">Create a MOVEit Transfer - Azure AD integration test user</span><span class="sxs-lookup"><span data-stu-id="c7feb-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="c7feb-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c7feb-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="c7feb-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span><span class="sxs-lookup"><span data-stu-id="c7feb-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="c7feb-222">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="c7feb-222">There is no action item for you in this section.</span></span> <span data-ttu-id="c7feb-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="c7feb-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="c7feb-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="c7feb-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c7feb-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c7feb-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="c7feb-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="c7feb-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c7feb-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c7feb-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="c7feb-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c7feb-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![The MOVEit Transfer - Azure AD integration link in the Applications list](./media/moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

1. <span data-ttu-id="c7feb-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c7feb-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c7feb-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c7feb-235">Click **Add** button.</span></span> <span data-ttu-id="c7feb-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c7feb-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c7feb-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c7feb-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c7feb-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c7feb-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c7feb-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c7feb-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c7feb-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c7feb-241">Test single sign-on</span></span>

<span data-ttu-id="c7feb-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c7feb-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c7feb-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span><span class="sxs-lookup"><span data-stu-id="c7feb-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7feb-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c7feb-244">Additional resources</span></span>

* [<span data-ttu-id="c7feb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7feb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c7feb-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7feb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/moveittransfer-tutorial/tutorial_general_203.png

