---
title: 'Tutorial: Azure Active Directory integration with TOPdesk - Public | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TOPdesk - Public.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ce74d4263e06c33c9beb66417b5ab8d61b8a259f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868413"
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="0a5e3-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="0a5e3-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="0a5e3-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a5e3-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a5e3-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a5e3-106">You can control in Azure AD who has access to TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="0a5e3-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0a5e3-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0a5e3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0a5e3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a5e3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a5e3-110">Prerequisites</span></span>

<span data-ttu-id="0a5e3-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="0a5e3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0a5e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a5e3-113">A TOPdesk - Public single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0a5e3-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a5e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a5e3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a5e3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a5e3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a5e3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a5e3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0a5e3-118">Scenario description</span></span>
<span data-ttu-id="0a5e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a5e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a5e3-121">Adding TOPdesk - Public from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a5e3-121">Adding TOPdesk - Public from the gallery</span></span>
1. <span data-ttu-id="0a5e3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="0a5e3-123">Adding TOPdesk - Public from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a5e3-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="0a5e3-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a5e3-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5e3-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5e3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="0a5e3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a5e3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="0a5e3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="0a5e3-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Public in the results list](./media/topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0a5e3-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5e3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0a5e3-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a5e3-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a5e3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="0a5e3-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="0a5e3-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a5e3-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a5e3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0a5e3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0a5e3-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0a5e3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0a5e3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0a5e3-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5e3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0a5e3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="0a5e3-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5e3-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5e3-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="0a5e3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

1. <span data-ttu-id="0a5e3-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![TOPdesk - Public Domain and URLs single sign-on information](./media/topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="0a5e3-155">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-155">a.</span></span> <span data-ttu-id="0a5e3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="0a5e3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="0a5e3-157">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-157">b.</span></span> <span data-ttu-id="0a5e3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="0a5e3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="0a5e3-159">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-159">c.</span></span> <span data-ttu-id="0a5e3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="0a5e3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0a5e3-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-161">These values are not real.</span></span> <span data-ttu-id="0a5e3-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0a5e3-163">Reply URL is explaned later in tutorial.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="0a5e3-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

1. <span data-ttu-id="0a5e3-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

1. <span data-ttu-id="0a5e3-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/topdesk-public-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="0a5e3-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a5e3-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0a5e3-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TOPdesk - Public Configuration](./media/topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

1. <span data-ttu-id="0a5e3-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

1. <span data-ttu-id="0a5e3-173">In the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="0a5e3-174">![Settings](./media/topdesk-public-tutorial/ic790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-174">![Settings](./media/topdesk-public-tutorial/ic790598.png "Settings")</span></span>

1. <span data-ttu-id="0a5e3-175">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="0a5e3-176">![Login Settings](./media/topdesk-public-tutorial/ic790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-176">![Login Settings](./media/topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

1. <span data-ttu-id="0a5e3-177">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="0a5e3-178">![General](./media/topdesk-public-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-178">![General](./media/topdesk-public-tutorial/ic790600.png "General")</span></span>

1. <span data-ttu-id="0a5e3-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="0a5e3-180">![Technical Settings](./media/topdesk-public-tutorial/ic790601.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-180">![Technical Settings](./media/topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="0a5e3-181">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-181">a.</span></span> <span data-ttu-id="0a5e3-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="0a5e3-183">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-183">b.</span></span> <span data-ttu-id="0a5e3-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="0a5e3-185">![AssertionConsumerService](./media/topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-185">![AssertionConsumerService](./media/topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="0a5e3-186">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-186">c.</span></span> <span data-ttu-id="0a5e3-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
1. <span data-ttu-id="0a5e3-188">To create a certificate file, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="0a5e3-189">![Certificate](./media/topdesk-public-tutorial/ic790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-189">![Certificate](./media/topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="0a5e3-190">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-190">a.</span></span> <span data-ttu-id="0a5e3-191">Open the downloaded metadata file from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="0a5e3-192">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-192">b.</span></span> <span data-ttu-id="0a5e3-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="0a5e3-194">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-194">c.</span></span> <span data-ttu-id="0a5e3-195">Copy the value of the **X509Certificate** node.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="0a5e3-196">d.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-196">d.</span></span> <span data-ttu-id="0a5e3-197">Save the copied **X509Certificate** value locally on your computer in a file.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

1. <span data-ttu-id="0a5e3-198">In the **Public** section, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="0a5e3-199">![SAML Login](./media/topdesk-public-tutorial/ic790625.png "SAML Login")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-199">![SAML Login](./media/topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

1. <span data-ttu-id="0a5e3-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="0a5e3-201">![SAML Configuration Assistant](./media/topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-201">![SAML Configuration Assistant](./media/topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="0a5e3-202">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-202">a.</span></span> <span data-ttu-id="0a5e3-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="0a5e3-204">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-204">b.</span></span> <span data-ttu-id="0a5e3-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="0a5e3-206">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-206">c.</span></span> <span data-ttu-id="0a5e3-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="0a5e3-208">d.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-208">d.</span></span> <span data-ttu-id="0a5e3-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="0a5e3-210">e.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-210">e.</span></span> <span data-ttu-id="0a5e3-211">In the **Display name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0a5e3-212">f.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-212">f.</span></span> <span data-ttu-id="0a5e3-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0a5e3-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0a5e3-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a5e3-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a5e3-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a5e3-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0a5e3-217">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a5e3-217">Create an Azure AD test user</span></span>

<span data-ttu-id="0a5e3-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="0a5e3-220">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5e3-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5e3-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/topdesk-public-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="0a5e3-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/topdesk-public-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="0a5e3-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/topdesk-public-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="0a5e3-227">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-227">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0a5e3-229">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-229">a.</span></span> <span data-ttu-id="0a5e3-230">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a5e3-231">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-231">b.</span></span> <span data-ttu-id="0a5e3-232">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0a5e3-233">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-233">c.</span></span> <span data-ttu-id="0a5e3-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0a5e3-235">d.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-235">d.</span></span> <span data-ttu-id="0a5e3-236">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="0a5e3-237">Create a TOPdesk - Public test user</span><span class="sxs-lookup"><span data-stu-id="0a5e3-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="0a5e3-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="0a5e3-239">In the case of TOPdesk - Public, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="0a5e3-240">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="0a5e3-241">Sign on to your **TOPdesk - Public** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

1. <span data-ttu-id="0a5e3-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="0a5e3-243">![Person](./media/topdesk-public-tutorial/ic790628.png "Person")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-243">![Person](./media/topdesk-public-tutorial/ic790628.png "Person")</span></span>

1. <span data-ttu-id="0a5e3-244">On the New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a5e3-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="0a5e3-245">![New Person](./media/topdesk-public-tutorial/ic790629.png "New Person")</span><span class="sxs-lookup"><span data-stu-id="0a5e3-245">![New Person](./media/topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="0a5e3-246">a.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-246">a.</span></span> <span data-ttu-id="0a5e3-247">Click the General tab.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-247">Click the General tab.</span></span>

    <span data-ttu-id="0a5e3-248">b.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-248">b.</span></span> <span data-ttu-id="0a5e3-249">In the **Surname** textbox, type Surname of the user like Simon</span><span class="sxs-lookup"><span data-stu-id="0a5e3-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="0a5e3-250">c.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-250">c.</span></span> <span data-ttu-id="0a5e3-251">Select a **Site** for the account.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="0a5e3-252">d.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-252">d.</span></span> <span data-ttu-id="0a5e3-253">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0a5e3-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0a5e3-255">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a5e3-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="0a5e3-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Assign the user role][200] 

<span data-ttu-id="0a5e3-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a5e3-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5e3-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0a5e3-261">In the applications list, select **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![The TOPdesk - Public link in the Applications list](./media/topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

1. <span data-ttu-id="0a5e3-263">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-263">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="0a5e3-265">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-265">Click **Add** button.</span></span> <span data-ttu-id="0a5e3-266">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="0a5e3-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0a5e3-269">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-269">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0a5e3-270">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0a5e3-271">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a5e3-271">Test single sign-on</span></span>

<span data-ttu-id="0a5e3-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a5e3-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span><span class="sxs-lookup"><span data-stu-id="0a5e3-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="0a5e3-274">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a5e3-274">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a5e3-275">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0a5e3-275">Additional resources</span></span>

* [<span data-ttu-id="0a5e3-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a5e3-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0a5e3-277">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a5e3-277">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/topdesk-public-tutorial/tutorial_general_203.png

