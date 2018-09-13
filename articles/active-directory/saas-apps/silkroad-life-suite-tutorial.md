---
title: 'Tutorial: Azure Active Directory integration with SilkRoad Life Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SilkRoad Life Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: jeedes
ms.openlocfilehash: 4d8be22a6b700d5ea9d95ee19d6ad3fa7bf5910a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857248"
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="42138-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="42138-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>

<span data-ttu-id="42138-104">In this tutorial, you learn how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42138-104">In this tutorial, you learn how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42138-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="42138-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42138-106">You can control in Azure AD who has access to SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="42138-106">You can control in Azure AD who has access to SilkRoad Life Suite.</span></span>
- <span data-ttu-id="42138-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="42138-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="42138-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="42138-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="42138-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42138-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42138-110">Prerequisites</span></span>

<span data-ttu-id="42138-111">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="42138-111">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

- <span data-ttu-id="42138-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="42138-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42138-113">A SilkRoad Life Suite single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="42138-113">A SilkRoad Life Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42138-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="42138-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42138-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="42138-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42138-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="42138-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42138-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42138-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42138-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="42138-118">Scenario description</span></span>
<span data-ttu-id="42138-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="42138-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42138-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="42138-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42138-121">Adding SilkRoad Life Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="42138-121">Adding SilkRoad Life Suite from the gallery</span></span>
1. <span data-ttu-id="42138-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42138-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="42138-123">Adding SilkRoad Life Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="42138-123">Adding SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="42138-124">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="42138-124">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42138-125">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42138-125">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42138-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="42138-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="42138-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="42138-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42138-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42138-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="42138-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="42138-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="42138-133">In the search box, type **SilkRoad Life Suite**, select **SilkRoad Life Suite** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="42138-133">In the search box, type **SilkRoad Life Suite**, select **SilkRoad Life Suite** from result panel then click **Add** button to add the application.</span></span>

    ![SilkRoad Life Suite in the results list](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="42138-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42138-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="42138-136">In this section, you configure and test Azure AD single sign-on with SilkRoad Life Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42138-136">In this section, you configure and test Azure AD single sign-on with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42138-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42138-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite is to a user in Azure AD.</span></span> <span data-ttu-id="42138-138">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="42138-138">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="42138-139">In SilkRoad Life Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="42138-139">In SilkRoad Life Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42138-140">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="42138-140">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42138-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="42138-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="42138-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42138-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="42138-143">**[Create a SilkRoad Life Suite test user](#create-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="42138-143">**[Create a SilkRoad Life Suite test user](#create-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="42138-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42138-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="42138-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="42138-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="42138-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42138-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="42138-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SilkRoad Life Suite application.</span><span class="sxs-lookup"><span data-stu-id="42138-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="42138-148">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42138-148">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="42138-149">In the Azure portal, on the **SilkRoad Life Suite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="42138-149">In the Azure portal, on the **SilkRoad Life Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="42138-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42138-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_samlbase.png)

1. <span data-ttu-id="42138-153">On the **SilkRoad Life Suite Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42138-153">On the **SilkRoad Life Suite Domain and URLs** section, perform the following steps:</span></span>

    ![SilkRoad Life Suite Domain and URLs single sign-on information](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_url1.png)

    <span data-ttu-id="42138-155">a.</span><span class="sxs-lookup"><span data-stu-id="42138-155">a.</span></span> <span data-ttu-id="42138-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.silkroad-eng.com/Authentication/`</span><span class="sxs-lookup"><span data-stu-id="42138-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.silkroad-eng.com/Authentication/`</span></span>

    <span data-ttu-id="42138-157">b.</span><span class="sxs-lookup"><span data-stu-id="42138-157">b.</span></span> <span data-ttu-id="42138-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="42138-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.silkroad-eng.com/Authentication/SP` |
    | `https://<subdomain>.silkroad.com/Authentication/SP` |

    <span data-ttu-id="42138-159">c.</span><span class="sxs-lookup"><span data-stu-id="42138-159">c.</span></span> <span data-ttu-id="42138-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="42138-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.silkroad-eng.com/Authentication/` |
    | `https://<subdomain>.silkroad.com/Authentication/` |
     
    > [!NOTE] 
    > <span data-ttu-id="42138-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="42138-161">These values are not real.</span></span> <span data-ttu-id="42138-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="42138-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="42138-163">Contact [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="42138-163">Contact [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to get these values.</span></span> 

1. <span data-ttu-id="42138-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="42138-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_certificate.png) 

1. <span data-ttu-id="42138-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="42138-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/silkroad-life-suite-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="42138-168">On the **SilkRoad Life Suite Configuration** section, click **Configure SilkRoad Life Suite** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="42138-168">On the **SilkRoad Life Suite Configuration** section, click **Configure SilkRoad Life Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42138-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="42138-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SilkRoad Life Suite Configuration](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_configure.png) 

1. <span data-ttu-id="42138-171">Sign-on to your SilkRoad company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="42138-171">Sign-on to your SilkRoad company site as administrator.</span></span> 
 
    >[!NOTE] 
    > <span data-ttu-id="42138-172">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span><span class="sxs-lookup"><span data-stu-id="42138-172">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>

1. <span data-ttu-id="42138-173">Go to **Service Provider**, and then click **Federation Details**.</span><span class="sxs-lookup"><span data-stu-id="42138-173">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

1. <span data-ttu-id="42138-175">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="42138-175">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD Single Sign-On][11] 

1. <span data-ttu-id="42138-177">In your **SilkRoad** application, click **Authentication Sources**.</span><span class="sxs-lookup"><span data-stu-id="42138-177">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD Single Sign-On][12] 

1. <span data-ttu-id="42138-179">Click **Add Authentication Source**.</span><span class="sxs-lookup"><span data-stu-id="42138-179">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD Single Sign-On][13] 

1. <span data-ttu-id="42138-181">In the **Add Authentication Source** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42138-181">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD Single Sign-On][14]
  
    <span data-ttu-id="42138-183">a.</span><span class="sxs-lookup"><span data-stu-id="42138-183">a.</span></span> <span data-ttu-id="42138-184">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-184">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file from Azure portal.</span></span>
  
    <span data-ttu-id="42138-185">b.</span><span class="sxs-lookup"><span data-stu-id="42138-185">b.</span></span> <span data-ttu-id="42138-186">Click **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="42138-186">Click **Create Identity Provider using File Data**.</span></span>

1. <span data-ttu-id="42138-187">In the **Authentication Sources** section, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="42138-187">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD Single Sign-On][15] 

1. <span data-ttu-id="42138-189">On the **Edit Authentication Source** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42138-189">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD Single Sign-On][16] 

    <span data-ttu-id="42138-191">a.</span><span class="sxs-lookup"><span data-stu-id="42138-191">a.</span></span> <span data-ttu-id="42138-192">As **Enabled**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="42138-192">As **Enabled**, select **Yes**.</span></span>

    <span data-ttu-id="42138-193">b.</span><span class="sxs-lookup"><span data-stu-id="42138-193">b.</span></span> <span data-ttu-id="42138-194">In the **EntityId** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-194">In the **EntityId** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="42138-195">c.</span><span class="sxs-lookup"><span data-stu-id="42138-195">c.</span></span> <span data-ttu-id="42138-196">In the **IdP Description** textbox, type a description for your configuration (for example: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="42138-196">In the **IdP Description** textbox, type a description for your configuration (for example: *Azure AD SSO*).</span></span>

    <span data-ttu-id="42138-197">d.</span><span class="sxs-lookup"><span data-stu-id="42138-197">d.</span></span> <span data-ttu-id="42138-198">In the **Metadata File** textbox, Upload the **metadata** file which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-198">In the **Metadata File** textbox, Upload the **metadata** file which you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="42138-199">e.</span><span class="sxs-lookup"><span data-stu-id="42138-199">e.</span></span> <span data-ttu-id="42138-200">In the **IdP Name** textbox, type a name that is specific to your configuration (for example: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="42138-200">In the **IdP Name** textbox, type a name that is specific to your configuration (for example: *Azure SP*).</span></span>
  
    <span data-ttu-id="42138-201">f.</span><span class="sxs-lookup"><span data-stu-id="42138-201">f.</span></span> <span data-ttu-id="42138-202">In the **Logout Service URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-202">In the **Logout Service URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="42138-203">g.</span><span class="sxs-lookup"><span data-stu-id="42138-203">g.</span></span> <span data-ttu-id="42138-204">In the **sign-on service URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42138-204">In the **sign-on service URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="42138-205">h.</span><span class="sxs-lookup"><span data-stu-id="42138-205">h.</span></span> <span data-ttu-id="42138-206">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="42138-206">Click **Save**.</span></span>

1. <span data-ttu-id="42138-207">Disable all other authentication sources.</span><span class="sxs-lookup"><span data-stu-id="42138-207">Disable all other authentication sources.</span></span> 
    
     ![Azure AD Single Sign-On][17]

> [!TIP]
> <span data-ttu-id="42138-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="42138-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42138-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="42138-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42138-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42138-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="42138-212">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42138-212">Create an Azure AD test user</span></span>

<span data-ttu-id="42138-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42138-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="42138-215">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42138-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42138-216">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="42138-216">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/silkroad-life-suite-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="42138-218">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="42138-218">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/silkroad-life-suite-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="42138-220">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="42138-220">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/silkroad-life-suite-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="42138-222">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42138-222">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/silkroad-life-suite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="42138-224">a.</span><span class="sxs-lookup"><span data-stu-id="42138-224">a.</span></span> <span data-ttu-id="42138-225">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42138-225">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42138-226">b.</span><span class="sxs-lookup"><span data-stu-id="42138-226">b.</span></span> <span data-ttu-id="42138-227">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42138-227">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="42138-228">c.</span><span class="sxs-lookup"><span data-stu-id="42138-228">c.</span></span> <span data-ttu-id="42138-229">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="42138-229">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="42138-230">d.</span><span class="sxs-lookup"><span data-stu-id="42138-230">d.</span></span> <span data-ttu-id="42138-231">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42138-231">Click **Create**.</span></span>
 
### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="42138-232">Create a SilkRoad Life Suite test user</span><span class="sxs-lookup"><span data-stu-id="42138-232">Create a SilkRoad Life Suite test user</span></span>

<span data-ttu-id="42138-233">In this section, you create a user called Britta Simon in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="42138-233">In this section, you create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="42138-234">Work with [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to add the users in the SilkRoad Life Suite platform.</span><span class="sxs-lookup"><span data-stu-id="42138-234">Work with [SilkRoad Life Suite Client support team](https://www.silkroad.com/locations/) to add the users in the SilkRoad Life Suite platform.</span></span> <span data-ttu-id="42138-235">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42138-235">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="42138-236">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42138-236">Assign the Azure AD test user</span></span>

<span data-ttu-id="42138-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="42138-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SilkRoad Life Suite.</span></span>

![Assign the user role][200] 

<span data-ttu-id="42138-239">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42138-239">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="42138-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42138-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="42138-242">In the applications list, select **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="42138-242">In the applications list, select **SilkRoad Life Suite**.</span></span>

    ![The SilkRoad Life Suite link in the Applications list](./media/silkroad-life-suite-tutorial/tutorial_silkroadlifesuite_app.png)  

1. <span data-ttu-id="42138-244">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="42138-244">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="42138-246">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="42138-246">Click **Add** button.</span></span> <span data-ttu-id="42138-247">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42138-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="42138-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="42138-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="42138-250">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="42138-250">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="42138-251">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42138-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="42138-252">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="42138-252">Test single sign-on</span></span>

<span data-ttu-id="42138-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="42138-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42138-254">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span><span class="sxs-lookup"><span data-stu-id="42138-254">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>
<span data-ttu-id="42138-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42138-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42138-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="42138-256">Additional resources</span></span>

* [<span data-ttu-id="42138-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42138-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="42138-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42138-258">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/silkroad-life-suite-tutorial/tutorial_general_04.png

[100]: ./media/silkroad-life-suite-tutorial/tutorial_general_100.png

[200]: ./media/silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/silkroad-life-suite-tutorial/tutorial_general_202.png
[203]: ./media/silkroad-life-suite-tutorial/tutorial_general_203.png
[10]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/silkroad-life-suite-tutorial/tutorial_silkroad_13.png
