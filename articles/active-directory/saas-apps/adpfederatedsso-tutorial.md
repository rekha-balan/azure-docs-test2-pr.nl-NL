---
title: 'Tutorial: Azure Active Directory integration with ADP | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ADP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7be5331b-0481-48f7-9d6b-619dfec657e1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2018
ms.author: jeedes
ms.openlocfilehash: 75b84c2856373126ceba0fc536e41d270f4d2d05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857015"
---
# <a name="tutorial-azure-active-directory-integration-with-adp"></a><span data-ttu-id="b9eca-103">Tutorial: Azure Active Directory integration with ADP</span><span class="sxs-lookup"><span data-stu-id="b9eca-103">Tutorial: Azure Active Directory integration with ADP</span></span>

<span data-ttu-id="b9eca-104">In this tutorial, you learn how to integrate ADP with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9eca-104">In this tutorial, you learn how to integrate ADP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9eca-105">Integrating ADP with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b9eca-105">Integrating ADP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9eca-106">You can control in Azure AD who has access to ADP.</span><span class="sxs-lookup"><span data-stu-id="b9eca-106">You can control in Azure AD who has access to ADP.</span></span>
- <span data-ttu-id="b9eca-107">You can enable your users to automatically get signed-on to ADP (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b9eca-107">You can enable your users to automatically get signed-on to ADP (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9eca-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9eca-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9eca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b9eca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9eca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9eca-110">Prerequisites</span></span>

<span data-ttu-id="b9eca-111">To configure Azure AD integration with ADP, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b9eca-111">To configure Azure AD integration with ADP, you need the following items:</span></span>

- <span data-ttu-id="b9eca-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b9eca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9eca-113">An ADP enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b9eca-113">An ADP enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9eca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b9eca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9eca-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b9eca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9eca-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b9eca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9eca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9eca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9eca-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b9eca-118">Scenario description</span></span>
<span data-ttu-id="b9eca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b9eca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9eca-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9eca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9eca-121">Adding ADP from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9eca-121">Adding ADP from the gallery</span></span>
2. <span data-ttu-id="b9eca-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9eca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-from-the-gallery"></a><span data-ttu-id="b9eca-123">Adding ADP from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9eca-123">Adding ADP from the gallery</span></span>
<span data-ttu-id="b9eca-124">To configure the integration of ADP into Azure AD, you need to add ADP from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b9eca-124">To configure the integration of ADP into Azure AD, you need to add ADP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9eca-125">**To add ADP from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9eca-125">**To add ADP from the gallery, perform the following steps:**</span></span>

1.  <span data-ttu-id="b9eca-126">Log on to your Microsoft Azure identity provider environment as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b9eca-126">Log on to your Microsoft Azure identity provider environment as an administrator.</span></span>

2. <span data-ttu-id="b9eca-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b9eca-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

3. <span data-ttu-id="b9eca-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9eca-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-130">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
4. <span data-ttu-id="b9eca-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

5. <span data-ttu-id="b9eca-134">In the search box, type **ADP**, select **ADP** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b9eca-134">In the search box, type **ADP**, select **ADP** from result panel then click **Add** button to add the application.</span></span>

    ![ADP in the results list](./media/adpfederatedsso-tutorial/tutorial_adp_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9eca-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9eca-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9eca-137">In this section, you configure and test Azure AD single sign-on with ADP based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b9eca-137">In this section, you configure and test Azure AD single sign-on with ADP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9eca-138">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9eca-138">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP is to a user in Azure AD.</span></span> <span data-ttu-id="b9eca-139">In other words, a link relationship between an Azure AD user and the related user in ADP needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b9eca-139">In other words, a link relationship between an Azure AD user and the related user in ADP needs to be established.</span></span>

<span data-ttu-id="b9eca-140">In ADP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b9eca-140">In ADP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9eca-141">To configure and test Azure AD single sign-on with ADP, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9eca-141">To configure and test Azure AD single sign-on with ADP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9eca-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b9eca-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9eca-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9eca-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9eca-144">**[Create an ADP test user](#create-an-adp-test-user)** - to have a counterpart of Britta Simon in ADP that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b9eca-144">**[Create an ADP test user](#create-an-adp-test-user)** - to have a counterpart of Britta Simon in ADP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9eca-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9eca-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9eca-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b9eca-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9eca-147">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9eca-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9eca-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP application.</span><span class="sxs-lookup"><span data-stu-id="b9eca-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP application.</span></span>

<span data-ttu-id="b9eca-149">**To configure Azure AD single sign-on with ADP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9eca-149">**To configure Azure AD single sign-on with ADP, perform the following steps:**</span></span>

1. <span data-ttu-id="b9eca-150">In the Azure portal, on the **ADP** application integration page, click on **Properties tab** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-150">In the Azure portal, on the **ADP** application integration page, click on **Properties tab** and perform the following steps:</span></span> 

    ![Single sign-on properties](./media/adpfederatedsso-tutorial/tutorial_adp_prop.png)

    <span data-ttu-id="b9eca-152">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-152">a.</span></span> <span data-ttu-id="b9eca-153">Set the **Enabled for users to sign-in** field value to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-153">Set the **Enabled for users to sign-in** field value to **Yes**.</span></span>

    <span data-ttu-id="b9eca-154">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-154">b.</span></span> <span data-ttu-id="b9eca-155">Copy the **User access URL** and you have to paste it in **Configure Sign-on URL section**, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9eca-155">Copy the **User access URL** and you have to paste it in **Configure Sign-on URL section**, which is explained later in the tutorial.</span></span>

    <span data-ttu-id="b9eca-156">c.</span><span class="sxs-lookup"><span data-stu-id="b9eca-156">c.</span></span> <span data-ttu-id="b9eca-157">Set the **User assignment required** field value to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-157">Set the **User assignment required** field value to **Yes**.</span></span>

    <span data-ttu-id="b9eca-158">d.</span><span class="sxs-lookup"><span data-stu-id="b9eca-158">d.</span></span> <span data-ttu-id="b9eca-159">Set the **Visible to users** field value to **No**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-159">Set the **Visible to users** field value to **No**.</span></span>

2. <span data-ttu-id="b9eca-160">Click **Single sign-on** on **ADP** application integration page.</span><span class="sxs-lookup"><span data-stu-id="b9eca-160">Click **Single sign-on** on **ADP** application integration page.</span></span>

    ![Configure single sign-on link][4]

3. <span data-ttu-id="b9eca-162">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9eca-162">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/adpfederatedsso-tutorial/tutorial_adp_samlbase.png)

4. <span data-ttu-id="b9eca-164">On the **ADP Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-164">On the **ADP Domain and URLs** section, perform the following steps:</span></span>

    ![ADP Domain and URLs single sign-on information](./media/adpfederatedsso-tutorial/tutorial_adp_url.png)

    <span data-ttu-id="b9eca-166">In the **Identifier** textbox, type a URL: `https://fed.adp.com`</span><span class="sxs-lookup"><span data-stu-id="b9eca-166">In the **Identifier** textbox, type a URL: `https://fed.adp.com`</span></span> 
    
5. <span data-ttu-id="b9eca-167">The ADP application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="b9eca-167">The ADP application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b9eca-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="b9eca-168">The following screenshot shows an example for this.</span></span> <span data-ttu-id="b9eca-169">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to **employeeid**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-169">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to **employeeid**.</span></span> 

    <span data-ttu-id="b9eca-170">Here the user mapping from Azure AD to ADP will be done on the **employeeid** but you can map this to a different value based on your application settings.</span><span class="sxs-lookup"><span data-stu-id="b9eca-170">Here the user mapping from Azure AD to ADP will be done on the **employeeid** but you can map this to a different value based on your application settings.</span></span> <span data-ttu-id="b9eca-171">So please work with [ADP support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span><span class="sxs-lookup"><span data-stu-id="b9eca-171">So please work with [ADP support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Configure Single Sign-On](./media/adpfederatedsso-tutorial/tutorial_adp_attribute.png)

6. <span data-ttu-id="b9eca-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="b9eca-174">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="b9eca-174">Attribute Name</span></span> | <span data-ttu-id="b9eca-175">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="b9eca-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="b9eca-176">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="b9eca-176">PersonImmutableID</span></span> | <span data-ttu-id="b9eca-177">user.employeeid</span><span class="sxs-lookup"><span data-stu-id="b9eca-177">user.employeeid</span></span> |
    
    <span data-ttu-id="b9eca-178">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-178">a.</span></span> <span data-ttu-id="b9eca-179">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/adpfederatedsso-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/adpfederatedsso-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b9eca-182">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-182">b.</span></span> <span data-ttu-id="b9eca-183">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b9eca-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b9eca-184">c.</span><span class="sxs-lookup"><span data-stu-id="b9eca-184">c.</span></span> <span data-ttu-id="b9eca-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b9eca-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b9eca-186">d.</span><span class="sxs-lookup"><span data-stu-id="b9eca-186">d.</span></span> <span data-ttu-id="b9eca-187">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-187">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9eca-188">Before you can configure the SAML assertion, you need to contact your [ADP  support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="b9eca-188">Before you can configure the SAML assertion, you need to contact your [ADP  support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="b9eca-189">You need this value to configure the custom claim for your application.</span><span class="sxs-lookup"><span data-stu-id="b9eca-189">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="b9eca-190">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b9eca-190">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/adpfederatedsso-tutorial/tutorial_adp_certificate.png) 

8. <span data-ttu-id="b9eca-192">To configure single sign-on on **ADP** side, you need to upload the downloaded **Metadata XML** on the [ADP website](https://adpfedsso.adp.com/public/login/index.fcc).</span><span class="sxs-lookup"><span data-stu-id="b9eca-192">To configure single sign-on on **ADP** side, you need to upload the downloaded **Metadata XML** on the [ADP website](https://adpfedsso.adp.com/public/login/index.fcc).</span></span>

> [!NOTE]  
> <span data-ttu-id="b9eca-193">This process may take a few days.</span><span class="sxs-lookup"><span data-stu-id="b9eca-193">This process may take a few days.</span></span> 

### <a name="configure-your-adp-services-for-federated-access"></a><span data-ttu-id="b9eca-194">Configure your ADP service(s) for federated access</span><span class="sxs-lookup"><span data-stu-id="b9eca-194">Configure your ADP service(s) for federated access</span></span>

>[!Important]
> <span data-ttu-id="b9eca-195">Your employees who require federated access to your ADP services must be assigned to the ADP service app and subsequently, users must be reassigned to the specific ADP service.</span><span class="sxs-lookup"><span data-stu-id="b9eca-195">Your employees who require federated access to your ADP services must be assigned to the ADP service app and subsequently, users must be reassigned to the specific ADP service.</span></span>
<span data-ttu-id="b9eca-196">Upon receipt of confirmation from your ADP representative, configure your ADP service(s) and assign/manage users to control user access to the specific ADP service.</span><span class="sxs-lookup"><span data-stu-id="b9eca-196">Upon receipt of confirmation from your ADP representative, configure your ADP service(s) and assign/manage users to control user access to the specific ADP service.</span></span>

1. <span data-ttu-id="b9eca-197">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b9eca-197">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b9eca-199">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-199">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9eca-200">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-200">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="b9eca-202">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-202">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b9eca-204">In the search box, type **ADP**, select **ADP** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b9eca-204">In the search box, type **ADP**, select **ADP** from result panel then click **Add** button to add the application.</span></span>

    ![ADP in the results list](./media/adpfederatedsso-tutorial/tutorial_adp_addservicegallery.png)

5. <span data-ttu-id="b9eca-206">In the Azure portal, on your **ADP** application integration page, click on **Properties tab** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-206">In the Azure portal, on your **ADP** application integration page, click on **Properties tab** and perform the following steps:</span></span>  

    ![Single sign-on linkedproperties](./media/adpfederatedsso-tutorial/tutorial_adp_linkedproperties.png)

    <span data-ttu-id="b9eca-208">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-208">a.</span></span>  <span data-ttu-id="b9eca-209">Set the **Enabled for users to sign-in** field value to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-209">Set the **Enabled for users to sign-in** field value to **Yes**.</span></span>

    <span data-ttu-id="b9eca-210">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-210">b.</span></span>  <span data-ttu-id="b9eca-211">Set the **User assignment required** field value to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-211">Set the **User assignment required** field value to **Yes**.</span></span>

    <span data-ttu-id="b9eca-212">c.</span><span class="sxs-lookup"><span data-stu-id="b9eca-212">c.</span></span>  <span data-ttu-id="b9eca-213">Set the **Visible to users** field value to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-213">Set the **Visible to users** field value to **Yes**.</span></span>

6. <span data-ttu-id="b9eca-214">Click **Single sign-on** on **ADP** application integration page.</span><span class="sxs-lookup"><span data-stu-id="b9eca-214">Click **Single sign-on** on **ADP** application integration page.</span></span>

    ![Configure single sign-on link][4]

7. <span data-ttu-id="b9eca-216">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-216">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span> <span data-ttu-id="b9eca-217">to link your application to **ADP**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-217">to link your application to **ADP**.</span></span>

    ![Single sign-on linked](./media/adpfederatedsso-tutorial/tutorial_adp_linked.png)

8. <span data-ttu-id="b9eca-219">Navigate to the **Configure Sign-on URL** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-219">Navigate to the **Configure Sign-on URL** section, perform the following steps:</span></span>

    ![Single sign-on prop](./media/adpfederatedsso-tutorial/tutorial_adp_linkedsignon.png)
                                                              
    <span data-ttu-id="b9eca-221">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-221">a.</span></span> <span data-ttu-id="b9eca-222">Paste the **User access URL**, which you have copied from above **properties tab** (from the main ADP app).</span><span class="sxs-lookup"><span data-stu-id="b9eca-222">Paste the **User access URL**, which you have copied from above **properties tab** (from the main ADP app).</span></span>
                                                             
    <span data-ttu-id="b9eca-223">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-223">b.</span></span> <span data-ttu-id="b9eca-224">Following are the 5 apps that support different **Relay State URLs**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-224">Following are the 5 apps that support different **Relay State URLs**.</span></span> <span data-ttu-id="b9eca-225">You have to append the appropriate **Relay State URL** value for particular application manually to the **User access URL**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-225">You have to append the appropriate **Relay State URL** value for particular application manually to the **User access URL**.</span></span>
    
    * <span data-ttu-id="b9eca-226">**ADP Workforce Now**</span><span class="sxs-lookup"><span data-stu-id="b9eca-226">**ADP Workforce Now**</span></span>
        
        `<User access URL>?relaystate=https://fed.adp.com/saml/fedlanding.html?WFN`

    * <span data-ttu-id="b9eca-227">**ADP Workforce Now Enhanced Time**</span><span class="sxs-lookup"><span data-stu-id="b9eca-227">**ADP Workforce Now Enhanced Time**</span></span>
        
        `<User access URL>?relaystate=https://fed.adp.com/saml/fedlanding.html?EETDC2`
    
    * <span data-ttu-id="b9eca-228">**ADP Vantage HCM**</span><span class="sxs-lookup"><span data-stu-id="b9eca-228">**ADP Vantage HCM**</span></span>
        
        `<User access URL>?relaystate=https://fed.adp.com/saml/fedlanding.html?ADPVANTAGE`

    * <span data-ttu-id="b9eca-229">**ADP Enterprise HR**</span><span class="sxs-lookup"><span data-stu-id="b9eca-229">**ADP Enterprise HR**</span></span>

        `<User access URL>?relaystate=https://fed.adp.com/saml/fedlanding.html?PORTAL`

    * <span data-ttu-id="b9eca-230">**MyADP**</span><span class="sxs-lookup"><span data-stu-id="b9eca-230">**MyADP**</span></span>

        `<User access URL>?relaystate=https://fed.adp.com/saml/fedlanding.html?REDBOX`

9. <span data-ttu-id="b9eca-231">**Save** your changes.</span><span class="sxs-lookup"><span data-stu-id="b9eca-231">**Save** your changes.</span></span>

10. <span data-ttu-id="b9eca-232">Upon receipt of confirmation from your ADP representative, begin test with one or two users.</span><span class="sxs-lookup"><span data-stu-id="b9eca-232">Upon receipt of confirmation from your ADP representative, begin test with one or two users.</span></span>

    <span data-ttu-id="b9eca-233">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-233">a.</span></span> <span data-ttu-id="b9eca-234">Assign few users to the ADP service App to test federated access.</span><span class="sxs-lookup"><span data-stu-id="b9eca-234">Assign few users to the ADP service App to test federated access.</span></span>

    <span data-ttu-id="b9eca-235">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-235">b.</span></span> <span data-ttu-id="b9eca-236">Test is successful when users access the ADP service app on the gallery and can access their ADP service.</span><span class="sxs-lookup"><span data-stu-id="b9eca-236">Test is successful when users access the ADP service app on the gallery and can access their ADP service.</span></span>
 
11. <span data-ttu-id="b9eca-237">On confirmation of a successful test, assign the federated ADP service to individual users or user groups, which is explained later in the tutorial and roll it out to your employees.</span><span class="sxs-lookup"><span data-stu-id="b9eca-237">On confirmation of a successful test, assign the federated ADP service to individual users or user groups, which is explained later in the tutorial and roll it out to your employees.</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9eca-238">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9eca-238">Create an Azure AD test user</span></span>

<span data-ttu-id="b9eca-239">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9eca-239">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b9eca-241">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9eca-241">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9eca-242">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b9eca-242">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/adpfederatedsso-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9eca-244">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-244">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/adpfederatedsso-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9eca-246">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b9eca-246">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/adpfederatedsso-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9eca-248">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9eca-248">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/adpfederatedsso-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9eca-250">a.</span><span class="sxs-lookup"><span data-stu-id="b9eca-250">a.</span></span> <span data-ttu-id="b9eca-251">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-251">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9eca-252">b.</span><span class="sxs-lookup"><span data-stu-id="b9eca-252">b.</span></span> <span data-ttu-id="b9eca-253">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9eca-253">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9eca-254">c.</span><span class="sxs-lookup"><span data-stu-id="b9eca-254">c.</span></span> <span data-ttu-id="b9eca-255">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b9eca-255">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9eca-256">d.</span><span class="sxs-lookup"><span data-stu-id="b9eca-256">d.</span></span> <span data-ttu-id="b9eca-257">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-257">Click **Create**.</span></span>
 
### <a name="create-an-adp-test-user"></a><span data-ttu-id="b9eca-258">Create an ADP test user</span><span class="sxs-lookup"><span data-stu-id="b9eca-258">Create an ADP test user</span></span>

<span data-ttu-id="b9eca-259">The objective of this section is to create a user called Britta Simon in ADP.</span><span class="sxs-lookup"><span data-stu-id="b9eca-259">The objective of this section is to create a user called Britta Simon in ADP.</span></span> <span data-ttu-id="b9eca-260">Work with [ADP support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP account.</span><span class="sxs-lookup"><span data-stu-id="b9eca-260">Work with [ADP support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9eca-261">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9eca-261">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9eca-262">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP.</span><span class="sxs-lookup"><span data-stu-id="b9eca-262">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b9eca-264">**To assign Britta Simon to ADP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9eca-264">**To assign Britta Simon to ADP, perform the following steps:**</span></span>

1. <span data-ttu-id="b9eca-265">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-265">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b9eca-267">In the applications list, select **ADP**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-267">In the applications list, select **ADP**.</span></span>

    ![The ADP link in the Applications list](./media/adpfederatedsso-tutorial/tutorial_adp_app.png)  

3. <span data-ttu-id="b9eca-269">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b9eca-269">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b9eca-271">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b9eca-271">Click **Add** button.</span></span> <span data-ttu-id="b9eca-272">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-272">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b9eca-274">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b9eca-274">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9eca-275">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-275">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9eca-276">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9eca-276">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9eca-277">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9eca-277">Test single sign-on</span></span>

<span data-ttu-id="b9eca-278">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b9eca-278">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9eca-279">When you click the ADP tile in the Access Panel, you should get automatically signed-on to your ADP application.</span><span class="sxs-lookup"><span data-stu-id="b9eca-279">When you click the ADP tile in the Access Panel, you should get automatically signed-on to your ADP application.</span></span>
<span data-ttu-id="b9eca-280">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9eca-280">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9eca-281">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b9eca-281">Additional resources</span></span>

* [<span data-ttu-id="b9eca-282">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9eca-282">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b9eca-283">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9eca-283">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/adpfederatedsso-tutorial/tutorial_general_01.png
[2]: ./media/adpfederatedsso-tutorial/tutorial_general_02.png
[3]: ./media/adpfederatedsso-tutorial/tutorial_general_03.png
[4]: ./media/adpfederatedsso-tutorial/tutorial_general_04.png

[100]: ./media/adpfederatedsso-tutorial/tutorial_general_100.png

[200]: ./media/adpfederatedsso-tutorial/tutorial_general_200.png
[201]: ./media/adpfederatedsso-tutorial/tutorial_general_201.png
[202]: ./media/adpfederatedsso-tutorial/tutorial_general_202.png
[203]: ./media/adpfederatedsso-tutorial/tutorial_general_203.png

