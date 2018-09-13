---
title: 'Tutorial: Azure Active Directory integration with Kanbanize | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kanbanize.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b436d2f6-bfa5-43fd-a8f9-d2144dc25669
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2018
ms.author: jeedes
ms.openlocfilehash: 746eaadcdb9a588087367c4c70237922cf0f14bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866212"
---
# <a name="tutorial-azure-active-directory-integration-with-kanbanize"></a><span data-ttu-id="1ac02-103">Tutorial: Azure Active Directory integration with Kanbanize</span><span class="sxs-lookup"><span data-stu-id="1ac02-103">Tutorial: Azure Active Directory integration with Kanbanize</span></span>

<span data-ttu-id="1ac02-104">In this tutorial, you learn how to integrate Kanbanize with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ac02-104">In this tutorial, you learn how to integrate Kanbanize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ac02-105">Integrating Kanbanize with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1ac02-105">Integrating Kanbanize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ac02-106">You can control in Azure AD who has access to Kanbanize.</span><span class="sxs-lookup"><span data-stu-id="1ac02-106">You can control in Azure AD who has access to Kanbanize.</span></span>
- <span data-ttu-id="1ac02-107">You can enable your users to automatically get signed-on to Kanbanize (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1ac02-107">You can enable your users to automatically get signed-on to Kanbanize (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1ac02-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ac02-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1ac02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1ac02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ac02-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1ac02-110">Prerequisites</span></span>

<span data-ttu-id="1ac02-111">To configure Azure AD integration with Kanbanize, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1ac02-111">To configure Azure AD integration with Kanbanize, you need the following items:</span></span>

- <span data-ttu-id="1ac02-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1ac02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ac02-113">A Kanbanize single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1ac02-113">A Kanbanize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ac02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1ac02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ac02-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1ac02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ac02-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1ac02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ac02-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ac02-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ac02-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1ac02-118">Scenario description</span></span>
<span data-ttu-id="1ac02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1ac02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ac02-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1ac02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ac02-121">Adding Kanbanize from the gallery</span><span class="sxs-lookup"><span data-stu-id="1ac02-121">Adding Kanbanize from the gallery</span></span>
2. <span data-ttu-id="1ac02-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1ac02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kanbanize-from-the-gallery"></a><span data-ttu-id="1ac02-123">Adding Kanbanize from the gallery</span><span class="sxs-lookup"><span data-stu-id="1ac02-123">Adding Kanbanize from the gallery</span></span>
<span data-ttu-id="1ac02-124">To configure the integration of Kanbanize into Azure AD, you need to add Kanbanize from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1ac02-124">To configure the integration of Kanbanize into Azure AD, you need to add Kanbanize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ac02-125">**To add Kanbanize from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1ac02-125">**To add Kanbanize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ac02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1ac02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="1ac02-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ac02-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="1ac02-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1ac02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="1ac02-133">In the search box, type **Kanbanize**, select **Kanbanize** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1ac02-133">In the search box, type **Kanbanize**, select **Kanbanize** from result panel then click **Add** button to add the application.</span></span>

    ![Kanbanize in the results list](./media/kanbanize-tutorial/tutorial_kanbanize_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1ac02-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1ac02-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1ac02-136">In this section, you configure and test Azure AD single sign-on with Kanbanize based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1ac02-136">In this section, you configure and test Azure AD single sign-on with Kanbanize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ac02-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Kanbanize is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ac02-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Kanbanize is to a user in Azure AD.</span></span> <span data-ttu-id="1ac02-138">In other words, a link relationship between an Azure AD user and the related user in Kanbanize needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1ac02-138">In other words, a link relationship between an Azure AD user and the related user in Kanbanize needs to be established.</span></span>

<span data-ttu-id="1ac02-139">To configure and test Azure AD single sign-on with Kanbanize, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1ac02-139">To configure and test Azure AD single sign-on with Kanbanize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ac02-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1ac02-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ac02-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ac02-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ac02-142">**[Create a Kanbanize test user](#create-a-kanbanize-test-user)** - to have a counterpart of Britta Simon in Kanbanize that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1ac02-142">**[Create a Kanbanize test user](#create-a-kanbanize-test-user)** - to have a counterpart of Britta Simon in Kanbanize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ac02-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ac02-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ac02-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1ac02-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1ac02-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1ac02-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1ac02-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kanbanize application.</span><span class="sxs-lookup"><span data-stu-id="1ac02-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kanbanize application.</span></span>

<span data-ttu-id="1ac02-147">**To configure Azure AD single sign-on with Kanbanize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1ac02-147">**To configure Azure AD single sign-on with Kanbanize, perform the following steps:**</span></span>

1. <span data-ttu-id="1ac02-148">In the Azure portal, on the **Kanbanize** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-148">In the Azure portal, on the **Kanbanize** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="1ac02-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ac02-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/kanbanize-tutorial/tutorial_kanbanize_samlbase.png)

3. <span data-ttu-id="1ac02-152">On the **Kanbanize Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="1ac02-152">On the **Kanbanize Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Kanbanize Domain and URLs single sign-on information](./media/kanbanize-tutorial/tutorial_kanbanize_url.png)

    <span data-ttu-id="1ac02-154">a.</span><span class="sxs-lookup"><span data-stu-id="1ac02-154">a.</span></span> <span data-ttu-id="1ac02-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/`</span><span class="sxs-lookup"><span data-stu-id="1ac02-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/`</span></span>

    <span data-ttu-id="1ac02-156">b.</span><span class="sxs-lookup"><span data-stu-id="1ac02-156">b.</span></span> <span data-ttu-id="1ac02-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="1ac02-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.kanbanize.com/saml/acs`</span></span>

    <span data-ttu-id="1ac02-158">c.</span><span class="sxs-lookup"><span data-stu-id="1ac02-158">c.</span></span> <span data-ttu-id="1ac02-159">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-159">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="1ac02-160">d.</span><span class="sxs-lookup"><span data-stu-id="1ac02-160">d.</span></span>  <span data-ttu-id="1ac02-161">In the **Relay State** textbox, type a URL: `/ctrl_login/saml_login`</span><span class="sxs-lookup"><span data-stu-id="1ac02-161">In the **Relay State** textbox, type a URL: `/ctrl_login/saml_login`</span></span>

    <span data-ttu-id="1ac02-162">e.</span><span class="sxs-lookup"><span data-stu-id="1ac02-162">e.</span></span> <span data-ttu-id="1ac02-163">If you wish to configure the application in **SP** initiated mode, in **Sign-on URL** textbox type a URL using the following pattern: `https://<subdomain>.kanbanize.com`</span><span class="sxs-lookup"><span data-stu-id="1ac02-163">If you wish to configure the application in **SP** initiated mode, in **Sign-on URL** textbox type a URL using the following pattern: `https://<subdomain>.kanbanize.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1ac02-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1ac02-164">These values are not real.</span></span> <span data-ttu-id="1ac02-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="1ac02-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1ac02-166">Contact [Kanbanize Client support team](mailto:support@ms.kanbanize.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1ac02-166">Contact [Kanbanize Client support team](mailto:support@ms.kanbanize.com) to get these values.</span></span> 

5. <span data-ttu-id="1ac02-167">Kanbanize application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="1ac02-167">Kanbanize application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="1ac02-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="1ac02-168">The following screenshot shows an example for this.</span></span> <span data-ttu-id="1ac02-169">The default value of **User Identifier** is **user.userprincipalname** but Kanbanize expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="1ac02-169">The default value of **User Identifier** is **user.userprincipalname** but Kanbanize expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="1ac02-170">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span><span class="sxs-lookup"><span data-stu-id="1ac02-170">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span>
    
    ![Configure Single Sign-On](./media/kanbanize-tutorial/tutorial_Kanbanize_attribute.png)

6. <span data-ttu-id="1ac02-172">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1ac02-172">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/kanbanize-tutorial/tutorial_kanbanize_certificate.png) 

7. <span data-ttu-id="1ac02-174">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1ac02-174">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/kanbanize-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="1ac02-176">On the **Kanbanize Configuration** section, click **Configure Kanbanize** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1ac02-176">On the **Kanbanize Configuration** section, click **Configure Kanbanize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ac02-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1ac02-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Kanbanize Configuration](./media/kanbanize-tutorial/tutorial_kanbanize_configure.png)

9. <span data-ttu-id="1ac02-179">In a different web browser window, login to Kanbanize as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="1ac02-179">In a different web browser window, login to Kanbanize as a Security Administrator.</span></span> 

10. <span data-ttu-id="1ac02-180">Go to top  right of the page, click on **Settings** logo.</span><span class="sxs-lookup"><span data-stu-id="1ac02-180">Go to top  right of the page, click on **Settings** logo.</span></span>

    ![Kanbanize settings](./media/kanbanize-tutorial/tutorial_kanbanize_set.png)

11. <span data-ttu-id="1ac02-182">On the Administration panel page from the left side of menu click **Integrations** and then enable **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-182">On the Administration panel page from the left side of menu click **Integrations** and then enable **Single Sign-On**.</span></span> 

    ![Kanbanize integrations](./media/kanbanize-tutorial/tutorial_kanbanize_admin.png)

12. <span data-ttu-id="1ac02-184">Under Integrations section, click on **CONFIGURE** to open **Single Sign-On Integration** page.</span><span class="sxs-lookup"><span data-stu-id="1ac02-184">Under Integrations section, click on **CONFIGURE** to open **Single Sign-On Integration** page.</span></span>

    ![Kanbanize config](./media/kanbanize-tutorial/tutorial_kanbanize_config.png)

13. <span data-ttu-id="1ac02-186">On the **Single Sign-On Integration** page under **Configurations**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1ac02-186">On the **Single Sign-On Integration** page under **Configurations**, perform the following steps:</span></span>

    ![Kanbanize integrations](./media/kanbanize-tutorial/tutorial_kanbanize_save.png)

    <span data-ttu-id="1ac02-188">a.</span><span class="sxs-lookup"><span data-stu-id="1ac02-188">a.</span></span> <span data-ttu-id="1ac02-189">In the **Idp Entity Id** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ac02-189">In the **Idp Entity Id** textbox, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1ac02-190">b.</span><span class="sxs-lookup"><span data-stu-id="1ac02-190">b.</span></span> <span data-ttu-id="1ac02-191">In the **Idp Login Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ac02-191">In the **Idp Login Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1ac02-192">c.</span><span class="sxs-lookup"><span data-stu-id="1ac02-192">c.</span></span> <span data-ttu-id="1ac02-193">In the **Idp Logout Endpoint** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ac02-193">In the **Idp Logout Endpoint** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="1ac02-194">d.</span><span class="sxs-lookup"><span data-stu-id="1ac02-194">d.</span></span> <span data-ttu-id="1ac02-195">In **Attribute name for Email** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="1ac02-195">In **Attribute name for Email** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="1ac02-196">e.</span><span class="sxs-lookup"><span data-stu-id="1ac02-196">e.</span></span> <span data-ttu-id="1ac02-197">In **Attribute name for First Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="1ac02-197">In **Attribute name for First Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>

    <span data-ttu-id="1ac02-198">f.</span><span class="sxs-lookup"><span data-stu-id="1ac02-198">f.</span></span> <span data-ttu-id="1ac02-199">In **Attribute name for Last Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="1ac02-199">In **Attribute name for Last Name** textbox, enter this value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span> 
    > [!Note]
    > <span data-ttu-id="1ac02-200">You can get these values by combining namespace and name values of the respective attribute from the User attributes section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1ac02-200">You can get these values by combining namespace and name values of the respective attribute from the User attributes section in Azure portal.</span></span>

    <span data-ttu-id="1ac02-201">g.</span><span class="sxs-lookup"><span data-stu-id="1ac02-201">g.</span></span> <span data-ttu-id="1ac02-202">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content (without the start and end markers), and then paste it into the **Idp X.509 Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="1ac02-202">In Notepad, open the base-64 encoded certificate that you downloaded from the Azure portal, copy its content (without the start and end markers), and then paste it into the **Idp X.509 Certificate** box.</span></span>

    <span data-ttu-id="1ac02-203">h.</span><span class="sxs-lookup"><span data-stu-id="1ac02-203">h.</span></span> <span data-ttu-id="1ac02-204">Check **Enable login with both SSO and Kanbanize**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-204">Check **Enable login with both SSO and Kanbanize**.</span></span>
    
    <span data-ttu-id="1ac02-205">i.</span><span class="sxs-lookup"><span data-stu-id="1ac02-205">i.</span></span> <span data-ttu-id="1ac02-206">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-206">Click **Save Settings**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1ac02-207">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1ac02-207">Create an Azure AD test user</span></span>

<span data-ttu-id="1ac02-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ac02-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1ac02-210">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1ac02-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ac02-211">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1ac02-211">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/kanbanize-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1ac02-213">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-213">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/kanbanize-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1ac02-215">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1ac02-215">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/kanbanize-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1ac02-217">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1ac02-217">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/kanbanize-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1ac02-219">a.</span><span class="sxs-lookup"><span data-stu-id="1ac02-219">a.</span></span> <span data-ttu-id="1ac02-220">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-220">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ac02-221">b.</span><span class="sxs-lookup"><span data-stu-id="1ac02-221">b.</span></span> <span data-ttu-id="1ac02-222">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ac02-222">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1ac02-223">c.</span><span class="sxs-lookup"><span data-stu-id="1ac02-223">c.</span></span> <span data-ttu-id="1ac02-224">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1ac02-224">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1ac02-225">d.</span><span class="sxs-lookup"><span data-stu-id="1ac02-225">d.</span></span> <span data-ttu-id="1ac02-226">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-226">Click **Create**.</span></span>
 
### <a name="create-a-kanbanize-test-user"></a><span data-ttu-id="1ac02-227">Create a Kanbanize test user</span><span class="sxs-lookup"><span data-stu-id="1ac02-227">Create a Kanbanize test user</span></span>

<span data-ttu-id="1ac02-228">The objective of this section is to create a user called Britta Simon in Kanbanize.</span><span class="sxs-lookup"><span data-stu-id="1ac02-228">The objective of this section is to create a user called Britta Simon in Kanbanize.</span></span> <span data-ttu-id="1ac02-229">Kanbanize supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1ac02-229">Kanbanize supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1ac02-230">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1ac02-230">There is no action item for you in this section.</span></span> <span data-ttu-id="1ac02-231">A new user is created during an attempt to access Kanbanize if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="1ac02-231">A new user is created during an attempt to access Kanbanize if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="1ac02-232">If you need to create a user manually, contact [Kanbanize Client support team](mailto:support@ms.kanbanize.com).</span><span class="sxs-lookup"><span data-stu-id="1ac02-232">If you need to create a user manually, contact [Kanbanize Client support team](mailto:support@ms.kanbanize.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1ac02-233">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1ac02-233">Assign the Azure AD test user</span></span>

<span data-ttu-id="1ac02-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kanbanize.</span><span class="sxs-lookup"><span data-stu-id="1ac02-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kanbanize.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1ac02-236">**To assign Britta Simon to Kanbanize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1ac02-236">**To assign Britta Simon to Kanbanize, perform the following steps:**</span></span>

1. <span data-ttu-id="1ac02-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="1ac02-239">In the applications list, select **Kanbanize**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-239">In the applications list, select **Kanbanize**.</span></span>

    ![The Kanbanize link in the Applications list](./media/kanbanize-tutorial/tutorial_kanbanize_app.png)  

3. <span data-ttu-id="1ac02-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1ac02-241">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="1ac02-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1ac02-243">Click **Add** button.</span></span> <span data-ttu-id="1ac02-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1ac02-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="1ac02-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1ac02-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ac02-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1ac02-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ac02-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1ac02-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1ac02-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1ac02-249">Test single sign-on</span></span>

<span data-ttu-id="1ac02-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1ac02-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ac02-251">When you click the Kanbanize tile in the Access Panel, you should get automatically signed-on to your Kanbanize application.</span><span class="sxs-lookup"><span data-stu-id="1ac02-251">When you click the Kanbanize tile in the Access Panel, you should get automatically signed-on to your Kanbanize application.</span></span>
<span data-ttu-id="1ac02-252">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ac02-252">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1ac02-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1ac02-253">Additional resources</span></span>

* [<span data-ttu-id="1ac02-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ac02-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1ac02-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ac02-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kanbanize-tutorial/tutorial_general_01.png
[2]: ./media/kanbanize-tutorial/tutorial_general_02.png
[3]: ./media/kanbanize-tutorial/tutorial_general_03.png
[4]: ./media/kanbanize-tutorial/tutorial_general_04.png

[100]: ./media/kanbanize-tutorial/tutorial_general_100.png

[200]: ./media/kanbanize-tutorial/tutorial_general_200.png
[201]: ./media/kanbanize-tutorial/tutorial_general_201.png
[202]: ./media/kanbanize-tutorial/tutorial_general_202.png
[203]: ./media/kanbanize-tutorial/tutorial_general_203.png

