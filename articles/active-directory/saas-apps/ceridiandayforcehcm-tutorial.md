---
title: 'Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Ceridian Dayforce HCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 6577955b275adfda3f0cfafe99a8f95efd16403c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866576"
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="2851e-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="2851e-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="2851e-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2851e-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2851e-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2851e-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2851e-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="2851e-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="2851e-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="2851e-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2851e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2851e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2851e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2851e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2851e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2851e-110">Prerequisites</span></span>

<span data-ttu-id="2851e-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2851e-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="2851e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2851e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2851e-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2851e-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2851e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2851e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2851e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2851e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2851e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2851e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2851e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2851e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2851e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2851e-118">Scenario description</span></span>
<span data-ttu-id="2851e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2851e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2851e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2851e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2851e-121">Adding Ceridian Dayforce HCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="2851e-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
1. <span data-ttu-id="2851e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2851e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="2851e-123">Adding Ceridian Dayforce HCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="2851e-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="2851e-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2851e-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2851e-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2851e-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2851e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2851e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="2851e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2851e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2851e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2851e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="2851e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="2851e-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2851e-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM in the results list](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2851e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2851e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2851e-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2851e-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2851e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2851e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="2851e-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2851e-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="2851e-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2851e-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2851e-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2851e-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2851e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2851e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2851e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2851e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2851e-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2851e-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2851e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2851e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2851e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2851e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2851e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2851e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2851e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="2851e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="2851e-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2851e-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="2851e-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2851e-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="2851e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2851e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

1. <span data-ttu-id="2851e-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2851e-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="2851e-155">a.</span><span class="sxs-lookup"><span data-stu-id="2851e-155">a.</span></span> <span data-ttu-id="2851e-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="2851e-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="2851e-157">Environment</span><span class="sxs-lookup"><span data-stu-id="2851e-157">Environment</span></span> | <span data-ttu-id="2851e-158">URL</span><span class="sxs-lookup"><span data-stu-id="2851e-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="2851e-159">For production</span><span class="sxs-lookup"><span data-stu-id="2851e-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="2851e-160">For test</span><span class="sxs-lookup"><span data-stu-id="2851e-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="2851e-161">b.</span><span class="sxs-lookup"><span data-stu-id="2851e-161">b.</span></span> <span data-ttu-id="2851e-162">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="2851e-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="2851e-163">Environment</span><span class="sxs-lookup"><span data-stu-id="2851e-163">Environment</span></span> | <span data-ttu-id="2851e-164">URL</span><span class="sxs-lookup"><span data-stu-id="2851e-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="2851e-165">For production</span><span class="sxs-lookup"><span data-stu-id="2851e-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="2851e-166">For test</span><span class="sxs-lookup"><span data-stu-id="2851e-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="2851e-167">c.</span><span class="sxs-lookup"><span data-stu-id="2851e-167">c.</span></span> <span data-ttu-id="2851e-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span><span class="sxs-lookup"><span data-stu-id="2851e-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="2851e-169">Environment</span><span class="sxs-lookup"><span data-stu-id="2851e-169">Environment</span></span> | <span data-ttu-id="2851e-170">URL</span><span class="sxs-lookup"><span data-stu-id="2851e-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="2851e-171">For production</span><span class="sxs-lookup"><span data-stu-id="2851e-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="2851e-172">For test</span><span class="sxs-lookup"><span data-stu-id="2851e-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="2851e-173">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2851e-173">These values are not real.</span></span> <span data-ttu-id="2851e-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="2851e-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="2851e-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="2851e-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/support) to get these values.</span></span>

1. <span data-ttu-id="2851e-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2851e-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

1. <span data-ttu-id="2851e-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="2851e-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2851e-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/support) first to identify the correct user identifier.</span><span class="sxs-lookup"><span data-stu-id="2851e-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/support) first to identify the correct user identifier.</span></span> <span data-ttu-id="2851e-180">Microsoft recommends using the **"name"** attribute as user identifier.</span><span class="sxs-lookup"><span data-stu-id="2851e-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="2851e-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="2851e-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="2851e-182">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="2851e-182">The following screenshot shows an example for this.</span></span>  

    ![Configure Single Sign-On](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

1. <span data-ttu-id="2851e-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2851e-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="2851e-185">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="2851e-185">Attribute Name</span></span>  | <span data-ttu-id="2851e-186">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="2851e-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="2851e-187">name</span><span class="sxs-lookup"><span data-stu-id="2851e-187">name</span></span>  | <span data-ttu-id="2851e-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="2851e-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="2851e-189">a.</span><span class="sxs-lookup"><span data-stu-id="2851e-189">a.</span></span> <span data-ttu-id="2851e-190">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2851e-193">b.</span><span class="sxs-lookup"><span data-stu-id="2851e-193">b.</span></span> <span data-ttu-id="2851e-194">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="2851e-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2851e-195">c.</span><span class="sxs-lookup"><span data-stu-id="2851e-195">c.</span></span> <span data-ttu-id="2851e-196">In the **Value** list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="2851e-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="2851e-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="2851e-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="2851e-198">d.</span><span class="sxs-lookup"><span data-stu-id="2851e-198">d.</span></span> <span data-ttu-id="2851e-199">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="2851e-199">Click **Ok**.</span></span>

1. <span data-ttu-id="2851e-200">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2851e-200">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="2851e-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2851e-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2851e-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="2851e-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM Configuration](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

1. <span data-ttu-id="2851e-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/support).</span><span class="sxs-lookup"><span data-stu-id="2851e-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/support).</span></span>

> [!TIP]
> <span data-ttu-id="2851e-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2851e-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2851e-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2851e-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2851e-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2851e-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2851e-209">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2851e-209">Create an Azure AD test user</span></span>

<span data-ttu-id="2851e-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2851e-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="2851e-212">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2851e-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2851e-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="2851e-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ceridiandayforcehcm-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="2851e-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2851e-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ceridiandayforcehcm-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="2851e-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2851e-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ceridiandayforcehcm-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="2851e-219">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2851e-219">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2851e-221">a.</span><span class="sxs-lookup"><span data-stu-id="2851e-221">a.</span></span> <span data-ttu-id="2851e-222">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2851e-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2851e-223">b.</span><span class="sxs-lookup"><span data-stu-id="2851e-223">b.</span></span> <span data-ttu-id="2851e-224">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2851e-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2851e-225">c.</span><span class="sxs-lookup"><span data-stu-id="2851e-225">c.</span></span> <span data-ttu-id="2851e-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="2851e-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2851e-227">d.</span><span class="sxs-lookup"><span data-stu-id="2851e-227">d.</span></span> <span data-ttu-id="2851e-228">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2851e-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="2851e-229">Create a Ceridian Dayforce HCM test user</span><span class="sxs-lookup"><span data-stu-id="2851e-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="2851e-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="2851e-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="2851e-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/support) to get users added in the Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="2851e-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/support) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2851e-232">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2851e-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2851e-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="2851e-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Assign User][200] 

<span data-ttu-id="2851e-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2851e-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="2851e-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2851e-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2851e-238">In the applications list, select **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="2851e-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configure Single Sign-On](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

1. <span data-ttu-id="2851e-240">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2851e-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2851e-242">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2851e-242">Click **Add** button.</span></span> <span data-ttu-id="2851e-243">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2851e-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2851e-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2851e-246">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-246">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2851e-247">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2851e-248">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2851e-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="2851e-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="2851e-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Assign the user role][200] 

<span data-ttu-id="2851e-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2851e-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="2851e-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2851e-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2851e-254">In the applications list, select **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="2851e-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![The Ceridian Dayforce HCM link in the Applications list](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

1. <span data-ttu-id="2851e-256">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2851e-256">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="2851e-258">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2851e-258">Click **Add** button.</span></span> <span data-ttu-id="2851e-259">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="2851e-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2851e-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2851e-262">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-262">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2851e-263">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2851e-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2851e-264">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2851e-264">Test single sign-on</span></span>

<span data-ttu-id="2851e-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2851e-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="2851e-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="2851e-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2851e-267">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2851e-267">Additional resources</span></span>

* [<span data-ttu-id="2851e-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2851e-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2851e-269">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2851e-269">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_203.png

