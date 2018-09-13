---
title: 'Tutorial: Azure Active Directory integration with Grovo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Grovo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 399cecc3-aa62-4914-8b6c-5a35289820c1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2018
ms.author: jeedes
ms.openlocfilehash: be49cbba53441124bd538a5d82e8c0e1d20d9e45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858076"
---
# <a name="tutorial-azure-active-directory-integration-with-grovo"></a><span data-ttu-id="23aca-103">Tutorial: Azure Active Directory integration with Grovo</span><span class="sxs-lookup"><span data-stu-id="23aca-103">Tutorial: Azure Active Directory integration with Grovo</span></span>

<span data-ttu-id="23aca-104">In this tutorial, you learn how to integrate Grovo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23aca-104">In this tutorial, you learn how to integrate Grovo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23aca-105">Integrating Grovo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="23aca-105">Integrating Grovo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23aca-106">You can control in Azure AD who has access to Grovo.</span><span class="sxs-lookup"><span data-stu-id="23aca-106">You can control in Azure AD who has access to Grovo.</span></span>
- <span data-ttu-id="23aca-107">You can enable your users to automatically get signed-on to Grovo (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="23aca-107">You can enable your users to automatically get signed-on to Grovo (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="23aca-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23aca-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="23aca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="23aca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23aca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="23aca-110">Prerequisites</span></span>

<span data-ttu-id="23aca-111">To configure Azure AD integration with Grovo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="23aca-111">To configure Azure AD integration with Grovo, you need the following items:</span></span>

- <span data-ttu-id="23aca-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="23aca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23aca-113">A Grovo single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="23aca-113">A Grovo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23aca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="23aca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23aca-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="23aca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23aca-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="23aca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23aca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23aca-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23aca-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="23aca-118">Scenario description</span></span>
<span data-ttu-id="23aca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="23aca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23aca-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="23aca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23aca-121">Adding Grovo from the gallery</span><span class="sxs-lookup"><span data-stu-id="23aca-121">Adding Grovo from the gallery</span></span>
1. <span data-ttu-id="23aca-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23aca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-grovo-from-the-gallery"></a><span data-ttu-id="23aca-123">Adding Grovo from the gallery</span><span class="sxs-lookup"><span data-stu-id="23aca-123">Adding Grovo from the gallery</span></span>
<span data-ttu-id="23aca-124">To configure the integration of Grovo into Azure AD, you need to add Grovo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="23aca-124">To configure the integration of Grovo into Azure AD, you need to add Grovo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23aca-125">**To add Grovo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23aca-125">**To add Grovo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23aca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="23aca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="23aca-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="23aca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23aca-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="23aca-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="23aca-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="23aca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="23aca-133">In the search box, type **Grovo**, select **Grovo** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="23aca-133">In the search box, type **Grovo**, select **Grovo** from result panel then click **Add** button to add the application.</span></span>

    ![Grovo in the results list](./media/grovo-tutorial/tutorial_grovo_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="23aca-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23aca-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="23aca-136">In this section, you configure and test Azure AD single sign-on with Grovo based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="23aca-136">In this section, you configure and test Azure AD single sign-on with Grovo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23aca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Grovo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23aca-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Grovo is to a user in Azure AD.</span></span> <span data-ttu-id="23aca-138">In other words, a link relationship between an Azure AD user and the related user in Grovo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="23aca-138">In other words, a link relationship between an Azure AD user and the related user in Grovo needs to be established.</span></span>

<span data-ttu-id="23aca-139">In Grovo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="23aca-139">In Grovo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="23aca-140">To configure and test Azure AD single sign-on with Grovo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="23aca-140">To configure and test Azure AD single sign-on with Grovo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23aca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="23aca-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="23aca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23aca-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="23aca-143">**[Create a Grovo test user](#create-a-grovo-test-user)** - to have a counterpart of Britta Simon in Grovo that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="23aca-143">**[Create a Grovo test user](#create-a-grovo-test-user)** - to have a counterpart of Britta Simon in Grovo that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="23aca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23aca-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="23aca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="23aca-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="23aca-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="23aca-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="23aca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Grovo application.</span><span class="sxs-lookup"><span data-stu-id="23aca-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Grovo application.</span></span>

<span data-ttu-id="23aca-148">**To configure Azure AD single sign-on with Grovo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23aca-148">**To configure Azure AD single sign-on with Grovo, perform the following steps:**</span></span>

1. <span data-ttu-id="23aca-149">In the Azure portal, on the **Grovo** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="23aca-149">In the Azure portal, on the **Grovo** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="23aca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23aca-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/grovo-tutorial/tutorial_grovo_samlbase.png)

1. <span data-ttu-id="23aca-153">On the **Grovo Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="23aca-153">On the **Grovo Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Grovo Domain and URLs single sign-on information](./media/grovo-tutorial/tutorial_grovo_url.png)

    <span data-ttu-id="23aca-155">a.</span><span class="sxs-lookup"><span data-stu-id="23aca-155">a.</span></span> <span data-ttu-id="23aca-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="23aca-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="23aca-157">b.</span><span class="sxs-lookup"><span data-stu-id="23aca-157">b.</span></span> <span data-ttu-id="23aca-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/saml-assertion`</span><span class="sxs-lookup"><span data-stu-id="23aca-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/saml-assertion`</span></span>

1. <span data-ttu-id="23aca-159">Check **Show advanced URL settings**, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="23aca-159">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![Grovo Domain and URLs single sign-on information](./media/grovo-tutorial/tutorial_grovo_url1.png)

    <span data-ttu-id="23aca-161">a.</span><span class="sxs-lookup"><span data-stu-id="23aca-161">a.</span></span> <span data-ttu-id="23aca-162">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.grovo.com`</span><span class="sxs-lookup"><span data-stu-id="23aca-162">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.grovo.com`</span></span>

    <span data-ttu-id="23aca-163">b.</span><span class="sxs-lookup"><span data-stu-id="23aca-163">b.</span></span> <span data-ttu-id="23aca-164">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23aca-164">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Grovo Domain and URLs single sign-on information](./media/grovo-tutorial/tutorial_grovo_url2.png)
    
    <span data-ttu-id="23aca-166">In the **Sign on URL** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/saml-assertion`</span><span class="sxs-lookup"><span data-stu-id="23aca-166">In the **Sign on URL** textbox, type a URL using the following pattern: `https://<subdomain>.grovo.com/sso/saml2/saml-assertion`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23aca-167">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="23aca-167">These values are not real.</span></span> <span data-ttu-id="23aca-168">Update these values with the actual Identifier, Reply URL, Sign on URL and Relay state.</span><span class="sxs-lookup"><span data-stu-id="23aca-168">Update these values with the actual Identifier, Reply URL, Sign on URL and Relay state.</span></span> <span data-ttu-id="23aca-169">Contact [Grovo support team](https://www.grovo.com/contact-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="23aca-169">Contact [Grovo support team](https://www.grovo.com/contact-us) to get these values.</span></span>
 
1. <span data-ttu-id="23aca-170">Grovo application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="23aca-170">Grovo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="23aca-171">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="23aca-171">Configure the following claims for this application.</span></span> <span data-ttu-id="23aca-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="23aca-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="23aca-173">Please map **User Identifier** with **user.mail** and configure other attributes as shown in below screenshot.</span><span class="sxs-lookup"><span data-stu-id="23aca-173">Please map **User Identifier** with **user.mail** and configure other attributes as shown in below screenshot.</span></span>
    
    ![Configure Single Sign-On attb](./media/grovo-tutorial/tutorial_grovo_attribute.png)
    
1. <span data-ttu-id="23aca-175">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23aca-175">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="23aca-176">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="23aca-176">Attribute Name</span></span> | <span data-ttu-id="23aca-177">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="23aca-177">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="23aca-178">First Name</span><span class="sxs-lookup"><span data-stu-id="23aca-178">First Name</span></span>          | <span data-ttu-id="23aca-179">user.givenname</span><span class="sxs-lookup"><span data-stu-id="23aca-179">user.givenname</span></span> |
    | <span data-ttu-id="23aca-180">Last Name</span><span class="sxs-lookup"><span data-stu-id="23aca-180">Last Name</span></span>           | <span data-ttu-id="23aca-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="23aca-181">user.surname</span></span> |
    | <span data-ttu-id="23aca-182">Email Address</span><span class="sxs-lookup"><span data-stu-id="23aca-182">Email Address</span></span>       | <span data-ttu-id="23aca-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="23aca-183">user.mail</span></span>    |
    | <span data-ttu-id="23aca-184">employeeID</span><span class="sxs-lookup"><span data-stu-id="23aca-184">employeeID</span></span>          | <span data-ttu-id="23aca-185">user.employeeid</span><span class="sxs-lookup"><span data-stu-id="23aca-185">user.employeeid</span></span> |

    <span data-ttu-id="23aca-186">a.</span><span class="sxs-lookup"><span data-stu-id="23aca-186">a.</span></span> <span data-ttu-id="23aca-187">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="23aca-187">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/grovo-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On Addattb](./media/grovo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="23aca-190">b.</span><span class="sxs-lookup"><span data-stu-id="23aca-190">b.</span></span> <span data-ttu-id="23aca-191">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="23aca-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="23aca-192">c.</span><span class="sxs-lookup"><span data-stu-id="23aca-192">c.</span></span> <span data-ttu-id="23aca-193">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="23aca-193">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="23aca-194">d.</span><span class="sxs-lookup"><span data-stu-id="23aca-194">d.</span></span> <span data-ttu-id="23aca-195">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="23aca-195">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="23aca-196">e.</span><span class="sxs-lookup"><span data-stu-id="23aca-196">e.</span></span> <span data-ttu-id="23aca-197">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="23aca-197">Click **Ok**.</span></span>


1. <span data-ttu-id="23aca-198">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="23aca-198">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/grovo-tutorial/tutorial_grovo_certificate.png) 

1. <span data-ttu-id="23aca-200">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="23aca-200">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/grovo-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="23aca-202">On the **Grovo Configuration** section, click **Configure Grovo** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="23aca-202">On the **Grovo Configuration** section, click **Configure Grovo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23aca-203">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="23aca-203">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Grovo Configuration](./media/grovo-tutorial/tutorial_grovo_configure.png) 

1. <span data-ttu-id="23aca-205">In a different web browser window, login to Grovo as Administrator.</span><span class="sxs-lookup"><span data-stu-id="23aca-205">In a different web browser window, login to Grovo as Administrator.</span></span>

1. <span data-ttu-id="23aca-206">Go to **Admin** > **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="23aca-206">Go to **Admin** > **Integrations**.</span></span>
 
    ![Grovo Configuration](./media/grovo-tutorial/tutorial_grovo_admin.png) 

1. <span data-ttu-id="23aca-208">Click **SET UP** under **SP Initiated SAML 2.0** section.</span><span class="sxs-lookup"><span data-stu-id="23aca-208">Click **SET UP** under **SP Initiated SAML 2.0** section.</span></span>

    ![Grovo Configuration](./media/grovo-tutorial/tutorial_grovo_setup.png)

1. <span data-ttu-id="23aca-210">In **SP Initiated SAML 2.0** popup window perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23aca-210">In **SP Initiated SAML 2.0** popup window perform the following steps:</span></span>

    ![Grovo Configuration](./media/grovo-tutorial/tutorial_grovo_saml.png)

    <span data-ttu-id="23aca-212">a.</span><span class="sxs-lookup"><span data-stu-id="23aca-212">a.</span></span> <span data-ttu-id="23aca-213">In the **Entity id** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23aca-213">In the **Entity id** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="23aca-214">b.</span><span class="sxs-lookup"><span data-stu-id="23aca-214">b.</span></span> <span data-ttu-id="23aca-215">In the **Single sign on service endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23aca-215">In the **Single sign on service endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="23aca-216">c.</span><span class="sxs-lookup"><span data-stu-id="23aca-216">c.</span></span> <span data-ttu-id="23aca-217">Select **Single sign on service endpoint binding** as `urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect`.</span><span class="sxs-lookup"><span data-stu-id="23aca-217">Select **Single sign on service endpoint binding** as `urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect`.</span></span>
    
    <span data-ttu-id="23aca-218">d.</span><span class="sxs-lookup"><span data-stu-id="23aca-218">d.</span></span> <span data-ttu-id="23aca-219">Open the downloaded **Base64 encoded certificate** from Azure portal in notepad, paste it into the **Public key** textbox.</span><span class="sxs-lookup"><span data-stu-id="23aca-219">Open the downloaded **Base64 encoded certificate** from Azure portal in notepad, paste it into the **Public key** textbox.</span></span>

    <span data-ttu-id="23aca-220">e.</span><span class="sxs-lookup"><span data-stu-id="23aca-220">e.</span></span> <span data-ttu-id="23aca-221">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="23aca-221">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="23aca-222">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="23aca-222">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23aca-223">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="23aca-223">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23aca-224">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23aca-224">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="23aca-225">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="23aca-225">Create an Azure AD test user</span></span>

<span data-ttu-id="23aca-226">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23aca-226">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="23aca-228">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23aca-228">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23aca-229">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="23aca-229">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/grovo-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="23aca-231">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="23aca-231">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/grovo-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="23aca-233">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="23aca-233">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/grovo-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="23aca-235">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="23aca-235">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/grovo-tutorial/create_aaduser_04.png)

    <span data-ttu-id="23aca-237">a.</span><span class="sxs-lookup"><span data-stu-id="23aca-237">a.</span></span> <span data-ttu-id="23aca-238">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23aca-238">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23aca-239">b.</span><span class="sxs-lookup"><span data-stu-id="23aca-239">b.</span></span> <span data-ttu-id="23aca-240">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23aca-240">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="23aca-241">c.</span><span class="sxs-lookup"><span data-stu-id="23aca-241">c.</span></span> <span data-ttu-id="23aca-242">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="23aca-242">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="23aca-243">d.</span><span class="sxs-lookup"><span data-stu-id="23aca-243">d.</span></span> <span data-ttu-id="23aca-244">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="23aca-244">Click **Create**.</span></span>
  
### <a name="create-a-grovo-test-user"></a><span data-ttu-id="23aca-245">Create a Grovo test user</span><span class="sxs-lookup"><span data-stu-id="23aca-245">Create a Grovo test user</span></span>

<span data-ttu-id="23aca-246">The objective of this section is to create a user called Britta Simon in Grovo.</span><span class="sxs-lookup"><span data-stu-id="23aca-246">The objective of this section is to create a user called Britta Simon in Grovo.</span></span> <span data-ttu-id="23aca-247">Grovo supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="23aca-247">Grovo supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="23aca-248">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="23aca-248">There is no action item for you in this section.</span></span> <span data-ttu-id="23aca-249">A new user is created during an attempt to access Grovo if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="23aca-249">A new user is created during an attempt to access Grovo if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="23aca-250">If you need to create a user manually, Contact [Grovo support team](https://www.grovo.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="23aca-250">If you need to create a user manually, Contact [Grovo support team](https://www.grovo.com/contact-us).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="23aca-251">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="23aca-251">Assign the Azure AD test user</span></span>

<span data-ttu-id="23aca-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Grovo.</span><span class="sxs-lookup"><span data-stu-id="23aca-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Grovo.</span></span>

![Assign the user role][200] 

<span data-ttu-id="23aca-254">**To assign Britta Simon to Grovo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="23aca-254">**To assign Britta Simon to Grovo, perform the following steps:**</span></span>

1. <span data-ttu-id="23aca-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="23aca-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="23aca-257">In the applications list, select **Grovo**.</span><span class="sxs-lookup"><span data-stu-id="23aca-257">In the applications list, select **Grovo**.</span></span>

    ![The Grovo link in the Applications list](./media/grovo-tutorial/tutorial_grovo_app.png)  

1. <span data-ttu-id="23aca-259">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="23aca-259">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="23aca-261">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="23aca-261">Click **Add** button.</span></span> <span data-ttu-id="23aca-262">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="23aca-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="23aca-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="23aca-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="23aca-265">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="23aca-265">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="23aca-266">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="23aca-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="23aca-267">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="23aca-267">Test single sign-on</span></span>

<span data-ttu-id="23aca-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="23aca-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23aca-269">When you click the Grovo tile in the Access Panel, you should get automatically signed-on to your Grovo application.</span><span class="sxs-lookup"><span data-stu-id="23aca-269">When you click the Grovo tile in the Access Panel, you should get automatically signed-on to your Grovo application.</span></span>
<span data-ttu-id="23aca-270">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23aca-270">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="23aca-271">Additional resources</span><span class="sxs-lookup"><span data-stu-id="23aca-271">Additional resources</span></span>

* [<span data-ttu-id="23aca-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23aca-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="23aca-273">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23aca-273">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/grovo-tutorial/tutorial_general_01.png
[2]: ./media/grovo-tutorial/tutorial_general_02.png
[3]: ./media/grovo-tutorial/tutorial_general_03.png
[4]: ./media/grovo-tutorial/tutorial_general_04.png

[100]: ./media/grovo-tutorial/tutorial_general_100.png

[200]: ./media/grovo-tutorial/tutorial_general_200.png
[201]: ./media/grovo-tutorial/tutorial_general_201.png
[202]: ./media/grovo-tutorial/tutorial_general_202.png
[203]: ./media/grovo-tutorial/tutorial_general_203.png

