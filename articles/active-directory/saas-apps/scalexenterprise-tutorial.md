---
title: 'Tutorial: Azure Active Directory integration with ScaleX Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 04708806b9e1ba224e7b438f11c68dca82d6320e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868713"
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="d44c0-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="d44c0-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="d44c0-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d44c0-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d44c0-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d44c0-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d44c0-106">You can control in Azure AD who has access to ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="d44c0-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="d44c0-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d44c0-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d44c0-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d44c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d44c0-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="d44c0-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="d44c0-110">What is application access and single sign-on with [Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d44c0-110">What is application access and single sign-on with [Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d44c0-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d44c0-111">Prerequisites</span></span>

<span data-ttu-id="d44c0-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d44c0-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="d44c0-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d44c0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d44c0-114">A ScaleX Enterprise single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d44c0-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d44c0-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d44c0-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d44c0-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d44c0-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d44c0-117">Do not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d44c0-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d44c0-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d44c0-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d44c0-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d44c0-119">Scenario description</span></span>
<span data-ttu-id="d44c0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d44c0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d44c0-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d44c0-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d44c0-122">Adding ScaleX Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="d44c0-122">Adding ScaleX Enterprise from the gallery</span></span>
1. <span data-ttu-id="d44c0-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d44c0-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="d44c0-124">Adding ScaleX Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="d44c0-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="d44c0-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d44c0-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d44c0-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d44c0-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d44c0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d44c0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d44c0-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d44c0-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d44c0-132">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d44c0-132">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d44c0-134">In the search box, type **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

1. <span data-ttu-id="d44c0-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d44c0-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d44c0-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d44c0-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d44c0-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d44c0-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d44c0-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d44c0-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="d44c0-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d44c0-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="d44c0-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d44c0-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="d44c0-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d44c0-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d44c0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d44c0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d44c0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d44c0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d44c0-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d44c0-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d44c0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d44c0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d44c0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d44c0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d44c0-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d44c0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d44c0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="d44c0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="d44c0-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d44c0-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="d44c0-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d44c0-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d44c0-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

1. <span data-ttu-id="d44c0-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d44c0-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="d44c0-158">a.</span><span class="sxs-lookup"><span data-stu-id="d44c0-158">a.</span></span> <span data-ttu-id="d44c0-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="d44c0-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="d44c0-160">b.</span><span class="sxs-lookup"><span data-stu-id="d44c0-160">b.</span></span> <span data-ttu-id="d44c0-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="d44c0-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

1. <span data-ttu-id="d44c0-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d44c0-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="d44c0-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="d44c0-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d44c0-165">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="d44c0-165">These are not the real values.</span></span> <span data-ttu-id="d44c0-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="d44c0-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="d44c0-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d44c0-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

1. <span data-ttu-id="d44c0-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="d44c0-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="d44c0-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span><span class="sxs-lookup"><span data-stu-id="d44c0-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="d44c0-171">a.</span><span class="sxs-lookup"><span data-stu-id="d44c0-171">a.</span></span> <span data-ttu-id="d44c0-172">Right click the attribute **name** and click delete.</span><span class="sxs-lookup"><span data-stu-id="d44c0-172">Right click the attribute **name** and click delete.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="d44c0-174">b.</span><span class="sxs-lookup"><span data-stu-id="d44c0-174">b.</span></span> <span data-ttu-id="d44c0-175">Click **emailaddress** attribute to open the Edit Attribute window.</span><span class="sxs-lookup"><span data-stu-id="d44c0-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="d44c0-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span><span class="sxs-lookup"><span data-stu-id="d44c0-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/edit_email_attribute.png) 
    
1. <span data-ttu-id="d44c0-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d44c0-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

1. <span data-ttu-id="d44c0-180">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d44c0-180">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="d44c0-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d44c0-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d44c0-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d44c0-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

1. <span data-ttu-id="d44c0-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d44c0-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

1. <span data-ttu-id="d44c0-186">Click the menu in the upper right and select **Contoso Administration**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d44c0-187">Contoso is just an example.</span><span class="sxs-lookup"><span data-stu-id="d44c0-187">Contoso is just an example.</span></span> <span data-ttu-id="d44c0-188">This should be your actual Company Name.</span><span class="sxs-lookup"><span data-stu-id="d44c0-188">This should be your actual Company Name.</span></span> 

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/Test_Admin.png) 

1. <span data-ttu-id="d44c0-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/admin_sso.png) 

1. <span data-ttu-id="d44c0-192">Complete the form as follows:</span><span class="sxs-lookup"><span data-stu-id="d44c0-192">Complete the form as follows:</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="d44c0-194">a.</span><span class="sxs-lookup"><span data-stu-id="d44c0-194">a.</span></span> <span data-ttu-id="d44c0-195">Select **“Create any user who can authenticate with SSO.”**</span><span class="sxs-lookup"><span data-stu-id="d44c0-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="d44c0-196">b.</span><span class="sxs-lookup"><span data-stu-id="d44c0-196">b.</span></span> <span data-ttu-id="d44c0-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span><span class="sxs-lookup"><span data-stu-id="d44c0-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="d44c0-198">c.</span><span class="sxs-lookup"><span data-stu-id="d44c0-198">c.</span></span> <span data-ttu-id="d44c0-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="d44c0-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="d44c0-200">d.</span><span class="sxs-lookup"><span data-stu-id="d44c0-200">d.</span></span> <span data-ttu-id="d44c0-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d44c0-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="d44c0-202">e.</span><span class="sxs-lookup"><span data-stu-id="d44c0-202">e.</span></span> <span data-ttu-id="d44c0-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d44c0-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="d44c0-204">f.</span><span class="sxs-lookup"><span data-stu-id="d44c0-204">f.</span></span> <span data-ttu-id="d44c0-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span><span class="sxs-lookup"><span data-stu-id="d44c0-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="d44c0-206">Ensure there are no line breaks in the middle of the certificate contents.</span><span class="sxs-lookup"><span data-stu-id="d44c0-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="d44c0-207">g.</span><span class="sxs-lookup"><span data-stu-id="d44c0-207">g.</span></span> <span data-ttu-id="d44c0-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="d44c0-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="d44c0-209">h.</span><span class="sxs-lookup"><span data-stu-id="d44c0-209">h.</span></span> <span data-ttu-id="d44c0-210">Click **Update SSO Settings** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="d44c0-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="d44c0-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d44c0-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d44c0-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d44c0-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d44c0-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d44c0-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d44c0-214">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d44c0-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="d44c0-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d44c0-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d44c0-217">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d44c0-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d44c0-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d44c0-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d44c0-220">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="d44c0-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d44c0-222">At the top of the dialog, click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="d44c0-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d44c0-224">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d44c0-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d44c0-226">a.</span><span class="sxs-lookup"><span data-stu-id="d44c0-226">a.</span></span> <span data-ttu-id="d44c0-227">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d44c0-228">b.</span><span class="sxs-lookup"><span data-stu-id="d44c0-228">b.</span></span> <span data-ttu-id="d44c0-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d44c0-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d44c0-230">c.</span><span class="sxs-lookup"><span data-stu-id="d44c0-230">c.</span></span> <span data-ttu-id="d44c0-231">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d44c0-232">d.</span><span class="sxs-lookup"><span data-stu-id="d44c0-232">d.</span></span> <span data-ttu-id="d44c0-233">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="d44c0-234">Creating a ScaleX Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="d44c0-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="d44c0-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d44c0-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="d44c0-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span><span class="sxs-lookup"><span data-stu-id="d44c0-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="d44c0-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span><span class="sxs-lookup"><span data-stu-id="d44c0-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d44c0-238">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d44c0-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d44c0-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d44c0-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Assign User][200] 

<span data-ttu-id="d44c0-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d44c0-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="d44c0-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d44c0-244">In the applications list, select **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Configure Single Sign-On](./media/scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

1. <span data-ttu-id="d44c0-246">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d44c0-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d44c0-248">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d44c0-248">Click **Add** button.</span></span> <span data-ttu-id="d44c0-249">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d44c0-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d44c0-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d44c0-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d44c0-252">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d44c0-252">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d44c0-253">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d44c0-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="d44c0-254">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d44c0-254">Testing single sign-on</span></span>

<span data-ttu-id="d44c0-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d44c0-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d44c0-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="d44c0-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="d44c0-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d44c0-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d44c0-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d44c0-258">Additional resources</span></span>

* [<span data-ttu-id="d44c0-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d44c0-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d44c0-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d44c0-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/scalexenterprise-tutorial/tutorial_general_203.png

