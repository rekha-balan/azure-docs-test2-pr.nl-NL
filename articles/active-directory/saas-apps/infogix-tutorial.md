---
title: 'Tutorial: Azure Active Directory integration with Infogix Data3Sixty Govern | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Infogix Data3Sixty Govern.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: aa3109b8-bdbe-45ae-933a-2eb4dc03855c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: jeedes
ms.openlocfilehash: 3e54ade44828bf1e26c310a14ae401fe8ae33229
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865935"
---
# <a name="tutorial-azure-active-directory-integration-with-infogix-data3sixty-govern"></a><span data-ttu-id="3acc8-103">Tutorial: Azure Active Directory integration with Infogix Data3Sixty Govern</span><span class="sxs-lookup"><span data-stu-id="3acc8-103">Tutorial: Azure Active Directory integration with Infogix Data3Sixty Govern</span></span>

<span data-ttu-id="3acc8-104">In this tutorial, you learn how to integrate Infogix Data3Sixty Govern with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3acc8-104">In this tutorial, you learn how to integrate Infogix Data3Sixty Govern with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3acc8-105">Integrating Infogix Data3Sixty Govern with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3acc8-105">Integrating Infogix Data3Sixty Govern with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3acc8-106">You can control in Azure AD who has access to Infogix Data3Sixty Govern.</span><span class="sxs-lookup"><span data-stu-id="3acc8-106">You can control in Azure AD who has access to Infogix Data3Sixty Govern.</span></span>
- <span data-ttu-id="3acc8-107">You can enable your users to automatically get signed-on to Infogix Data3Sixty Govern (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3acc8-107">You can enable your users to automatically get signed-on to Infogix Data3Sixty Govern (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3acc8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3acc8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3acc8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3acc8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3acc8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3acc8-110">Prerequisites</span></span>

<span data-ttu-id="3acc8-111">To configure Azure AD integration with Infogix Data3Sixty Govern, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3acc8-111">To configure Azure AD integration with Infogix Data3Sixty Govern, you need the following items:</span></span>

- <span data-ttu-id="3acc8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3acc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3acc8-113">An Infogix Data3Sixty Govern single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3acc8-113">An Infogix Data3Sixty Govern single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3acc8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3acc8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3acc8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3acc8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3acc8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3acc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3acc8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3acc8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3acc8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3acc8-118">Scenario description</span></span>
<span data-ttu-id="3acc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3acc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3acc8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3acc8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3acc8-121">Adding Infogix Data3Sixty Govern from the gallery</span><span class="sxs-lookup"><span data-stu-id="3acc8-121">Adding Infogix Data3Sixty Govern from the gallery</span></span>
1. <span data-ttu-id="3acc8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3acc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infogix-data3sixty-govern-from-the-gallery"></a><span data-ttu-id="3acc8-123">Adding Infogix Data3Sixty Govern from the gallery</span><span class="sxs-lookup"><span data-stu-id="3acc8-123">Adding Infogix Data3Sixty Govern from the gallery</span></span>
<span data-ttu-id="3acc8-124">To configure the integration of Infogix Data3Sixty Govern into Azure AD, you need to add Infogix Data3Sixty Govern from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3acc8-124">To configure the integration of Infogix Data3Sixty Govern into Azure AD, you need to add Infogix Data3Sixty Govern from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3acc8-125">**To add Infogix Data3Sixty Govern from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3acc8-125">**To add Infogix Data3Sixty Govern from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3acc8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3acc8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="3acc8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3acc8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="3acc8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3acc8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="3acc8-133">In the search box, type **Infogix Data3Sixty Govern**, select **Infogix Data3Sixty Govern** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3acc8-133">In the search box, type **Infogix Data3Sixty Govern**, select **Infogix Data3Sixty Govern** from result panel then click **Add** button to add the application.</span></span>

    ![Infogix Data3Sixty Govern in the results list](./media/infogix-tutorial/tutorial_infogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3acc8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3acc8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3acc8-136">In this section, you configure and test Azure AD single sign-on with Infogix Data3Sixty Govern based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3acc8-136">In this section, you configure and test Azure AD single sign-on with Infogix Data3Sixty Govern based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3acc8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infogix Data3Sixty Govern is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3acc8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infogix Data3Sixty Govern is to a user in Azure AD.</span></span> <span data-ttu-id="3acc8-138">In other words, a link relationship between an Azure AD user and the related user in Infogix Data3Sixty Govern needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3acc8-138">In other words, a link relationship between an Azure AD user and the related user in Infogix Data3Sixty Govern needs to be established.</span></span>

<span data-ttu-id="3acc8-139">To configure and test Azure AD single sign-on with Infogix Data3Sixty Govern, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3acc8-139">To configure and test Azure AD single sign-on with Infogix Data3Sixty Govern, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3acc8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3acc8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3acc8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3acc8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3acc8-142">**[Create an Infogix Data3Sixty Govern test user](#create-an-infogix-data3sixty-govern-test-user)** - to have a counterpart of Britta Simon in Infogix Data3Sixty Govern that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3acc8-142">**[Create an Infogix Data3Sixty Govern test user](#create-an-infogix-data3sixty-govern-test-user)** - to have a counterpart of Britta Simon in Infogix Data3Sixty Govern that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3acc8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3acc8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3acc8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3acc8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3acc8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3acc8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3acc8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infogix Data3Sixty Govern application.</span><span class="sxs-lookup"><span data-stu-id="3acc8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infogix Data3Sixty Govern application.</span></span>

<span data-ttu-id="3acc8-147">**To configure Azure AD single sign-on with Infogix Data3Sixty Govern, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3acc8-147">**To configure Azure AD single sign-on with Infogix Data3Sixty Govern, perform the following steps:**</span></span>

1. <span data-ttu-id="3acc8-148">In the Azure portal, on the **Infogix Data3Sixty Govern** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-148">In the Azure portal, on the **Infogix Data3Sixty Govern** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="3acc8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3acc8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/infogix-tutorial/tutorial_infogix_samlbase.png)

1. <span data-ttu-id="3acc8-152">On the **Infogix Data3Sixty Govern Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3acc8-152">On the **Infogix Data3Sixty Govern Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Infogix Data3Sixty Govern Domain and URLs single sign-on information](./media/infogix-tutorial/tutorial_infogix_url.png)

    <span data-ttu-id="3acc8-154">a.</span><span class="sxs-lookup"><span data-stu-id="3acc8-154">a.</span></span> <span data-ttu-id="3acc8-155">In the **Identifier** textbox, type a URL: `https://data3sixty.com/ui`</span><span class="sxs-lookup"><span data-stu-id="3acc8-155">In the **Identifier** textbox, type a URL: `https://data3sixty.com/ui`</span></span>

    <span data-ttu-id="3acc8-156">b.</span><span class="sxs-lookup"><span data-stu-id="3acc8-156">b.</span></span> <span data-ttu-id="3acc8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.data3sixty.com/sso/acs`</span><span class="sxs-lookup"><span data-stu-id="3acc8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.data3sixty.com/sso/acs`</span></span>

1. <span data-ttu-id="3acc8-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3acc8-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Infogix Data3Sixty Govern Domain and URLs single sign-on information](./media/infogix-tutorial/tutorial_infogix_url1.png)

    <span data-ttu-id="3acc8-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.data3sixty.com`</span><span class="sxs-lookup"><span data-stu-id="3acc8-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.data3sixty.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3acc8-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="3acc8-161">These values are not real.</span></span> <span data-ttu-id="3acc8-162">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="3acc8-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3acc8-163">Contact [Infogix Data3Sixty Govern Client support team](mailto:data3sixtysupport@infogix.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="3acc8-163">Contact [Infogix Data3Sixty Govern Client support team](mailto:data3sixtysupport@infogix.com) to get these values.</span></span>

1. <span data-ttu-id="3acc8-164">Infogix Data3Sixty Govern application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="3acc8-164">Infogix Data3Sixty Govern application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3acc8-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="3acc8-165">Configure the following claims for this application.</span></span> <span data-ttu-id="3acc8-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="3acc8-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="3acc8-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="3acc8-167">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On attb](./media/infogix-tutorial/tutorial_infogix_attribute.png)
    
1. <span data-ttu-id="3acc8-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3acc8-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3acc8-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="3acc8-170">Attribute Name</span></span> | <span data-ttu-id="3acc8-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="3acc8-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="3acc8-172">firstname</span><span class="sxs-lookup"><span data-stu-id="3acc8-172">firstname</span></span>           | <span data-ttu-id="3acc8-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3acc8-173">user.givenname</span></span> |
    | <span data-ttu-id="3acc8-174">lastname</span><span class="sxs-lookup"><span data-stu-id="3acc8-174">lastname</span></span>        | <span data-ttu-id="3acc8-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="3acc8-175">user.surname</span></span> |
    | <span data-ttu-id="3acc8-176">username</span><span class="sxs-lookup"><span data-stu-id="3acc8-176">username</span></span>       | <span data-ttu-id="3acc8-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="3acc8-177">user.mail</span></span>    |
    
    <span data-ttu-id="3acc8-178">a.</span><span class="sxs-lookup"><span data-stu-id="3acc8-178">a.</span></span> <span data-ttu-id="3acc8-179">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="3acc8-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/infogix-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On Addattb](./media/infogix-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3acc8-182">b.</span><span class="sxs-lookup"><span data-stu-id="3acc8-182">b.</span></span> <span data-ttu-id="3acc8-183">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3acc8-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3acc8-184">c.</span><span class="sxs-lookup"><span data-stu-id="3acc8-184">c.</span></span> <span data-ttu-id="3acc8-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3acc8-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3acc8-186">d.</span><span class="sxs-lookup"><span data-stu-id="3acc8-186">d.</span></span> <span data-ttu-id="3acc8-187">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="3acc8-187">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="3acc8-188">e.</span><span class="sxs-lookup"><span data-stu-id="3acc8-188">e.</span></span> <span data-ttu-id="3acc8-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-189">Click **Ok**.</span></span>

1. <span data-ttu-id="3acc8-190">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3acc8-190">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/infogix-tutorial/tutorial_infogix_certificate.png)

1. <span data-ttu-id="3acc8-192">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3acc8-192">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/infogix-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="3acc8-194">On the **Infogix Data3Sixty Govern Configuration** section, click **Configure Infogix Data3Sixty Govern** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3acc8-194">On the **Infogix Data3Sixty Govern Configuration** section, click **Configure Infogix Data3Sixty Govern** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3acc8-195">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3acc8-195">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Infogix Data3Sixty Govern Configuration](./media/infogix-tutorial/tutorial_infogix_configure.png) 

1. <span data-ttu-id="3acc8-197">To configure single sign-on on **Infogix Data3Sixty Govern** side, you need to send the downloaded **Certificate (Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Infogix Data3Sixty Govern support team](mailto:data3sixtysupport@infogix.com).</span><span class="sxs-lookup"><span data-stu-id="3acc8-197">To configure single sign-on on **Infogix Data3Sixty Govern** side, you need to send the downloaded **Certificate (Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Infogix Data3Sixty Govern support team](mailto:data3sixtysupport@infogix.com).</span></span> <span data-ttu-id="3acc8-198">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="3acc8-198">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3acc8-199">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3acc8-199">Create an Azure AD test user</span></span>

<span data-ttu-id="3acc8-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3acc8-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3acc8-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3acc8-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3acc8-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3acc8-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/infogix-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="3acc8-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/infogix-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="3acc8-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3acc8-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/infogix-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="3acc8-209">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3acc8-209">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/infogix-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3acc8-211">a.</span><span class="sxs-lookup"><span data-stu-id="3acc8-211">a.</span></span> <span data-ttu-id="3acc8-212">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3acc8-213">b.</span><span class="sxs-lookup"><span data-stu-id="3acc8-213">b.</span></span> <span data-ttu-id="3acc8-214">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3acc8-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3acc8-215">c.</span><span class="sxs-lookup"><span data-stu-id="3acc8-215">c.</span></span> <span data-ttu-id="3acc8-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3acc8-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3acc8-217">d.</span><span class="sxs-lookup"><span data-stu-id="3acc8-217">d.</span></span> <span data-ttu-id="3acc8-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-218">Click **Create**.</span></span>
 
### <a name="create-an-infogix-data3sixty-govern-test-user"></a><span data-ttu-id="3acc8-219">Create an Infogix Data3Sixty Govern test user</span><span class="sxs-lookup"><span data-stu-id="3acc8-219">Create an Infogix Data3Sixty Govern test user</span></span>


<span data-ttu-id="3acc8-220">The objective of this section is to create a user called Britta Simon in Infogix Data3Sixty Govern.</span><span class="sxs-lookup"><span data-stu-id="3acc8-220">The objective of this section is to create a user called Britta Simon in Infogix Data3Sixty Govern.</span></span> <span data-ttu-id="3acc8-221">Infogix Data3Sixty Govern supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="3acc8-221">Infogix Data3Sixty Govern supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3acc8-222">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="3acc8-222">There is no action item for you in this section.</span></span> <span data-ttu-id="3acc8-223">A new user is created during an attempt to access Infogix Data3Sixty Govern if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="3acc8-223">A new user is created during an attempt to access Infogix Data3Sixty Govern if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="3acc8-224">If you need to create a user manually, contact [Infogix Data3Sixty Govern support team](mailto:data3sixtysupport@infogix.com).</span><span class="sxs-lookup"><span data-stu-id="3acc8-224">If you need to create a user manually, contact [Infogix Data3Sixty Govern support team](mailto:data3sixtysupport@infogix.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3acc8-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3acc8-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="3acc8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infogix Data3Sixty Govern.</span><span class="sxs-lookup"><span data-stu-id="3acc8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infogix Data3Sixty Govern.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3acc8-228">**To assign Britta Simon to Infogix Data3Sixty Govern, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3acc8-228">**To assign Britta Simon to Infogix Data3Sixty Govern, perform the following steps:**</span></span>

1. <span data-ttu-id="3acc8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3acc8-231">In the applications list, select **Infogix Data3Sixty Govern**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-231">In the applications list, select **Infogix Data3Sixty Govern**.</span></span>

    ![The Infogix Data3Sixty Govern link in the Applications list](./media/infogix-tutorial/tutorial_infogix_app.png)  

1. <span data-ttu-id="3acc8-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3acc8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="3acc8-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3acc8-235">Click **Add** button.</span></span> <span data-ttu-id="3acc8-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3acc8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="3acc8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3acc8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3acc8-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3acc8-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3acc8-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3acc8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3acc8-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3acc8-241">Test single sign-on</span></span>

<span data-ttu-id="3acc8-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3acc8-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3acc8-243">When you click the Infogix Data3Sixty Govern tile in the Access Panel, you should get automatically signed-on to your Infogix Data3Sixty Govern application.</span><span class="sxs-lookup"><span data-stu-id="3acc8-243">When you click the Infogix Data3Sixty Govern tile in the Access Panel, you should get automatically signed-on to your Infogix Data3Sixty Govern application.</span></span>
<span data-ttu-id="3acc8-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3acc8-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3acc8-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3acc8-245">Additional resources</span></span>

* [<span data-ttu-id="3acc8-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3acc8-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3acc8-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3acc8-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/infogix-tutorial/tutorial_general_01.png
[2]: ./media/infogix-tutorial/tutorial_general_02.png
[3]: ./media/infogix-tutorial/tutorial_general_03.png
[4]: ./media/infogix-tutorial/tutorial_general_04.png

[100]: ./media/infogix-tutorial/tutorial_general_100.png

[200]: ./media/infogix-tutorial/tutorial_general_200.png
[201]: ./media/infogix-tutorial/tutorial_general_201.png
[202]: ./media/infogix-tutorial/tutorial_general_202.png
[203]: ./media/infogix-tutorial/tutorial_general_203.png

