---
title: 'Tutorial: Azure Active Directory integration with Tableau Server | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tableau Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 78f58f28eb9c25e0b5f6869f7e2348b41780fb60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969067"
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="0dbd8-103">Tutorial: Azure Active Directory integration with Tableau Server</span><span class="sxs-lookup"><span data-stu-id="0dbd8-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="0dbd8-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dbd8-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0dbd8-106">You can control in Azure AD who has access to Tableau Server</span><span class="sxs-lookup"><span data-stu-id="0dbd8-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="0dbd8-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0dbd8-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dbd8-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0dbd8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0dbd8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dbd8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0dbd8-110">Prerequisites</span></span>

<span data-ttu-id="0dbd8-111">To configure Azure AD integration with Tableau Server, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="0dbd8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0dbd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dbd8-113">A Tableau Server single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0dbd8-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dbd8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dbd8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dbd8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dbd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dbd8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0dbd8-118">Scenario description</span></span>
<span data-ttu-id="0dbd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dbd8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dbd8-121">Adding Tableau Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="0dbd8-121">Adding Tableau Server from the gallery</span></span>
1. <span data-ttu-id="0dbd8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0dbd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="0dbd8-123">Adding Tableau Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="0dbd8-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="0dbd8-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0dbd8-125">**To add Tableau Server from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0dbd8-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0dbd8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0dbd8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0dbd8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0dbd8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0dbd8-133">In the search box, type **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-133">In the search box, type **Tableau Server**.</span></span>

    ![Creating an Azure AD test user](./media/tableauserver-tutorial/tutorial_tableauserver_search.png)

1. <span data-ttu-id="0dbd8-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dbd8-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0dbd8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dbd8-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0dbd8-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0dbd8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="0dbd8-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="0dbd8-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0dbd8-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0dbd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0dbd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0dbd8-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0dbd8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0dbd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dbd8-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0dbd8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dbd8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="0dbd8-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0dbd8-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="0dbd8-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0dbd8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

1. <span data-ttu-id="0dbd8-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="0dbd8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-157">a.</span></span> <span data-ttu-id="0dbd8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="0dbd8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="0dbd8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-159">b.</span></span> <span data-ttu-id="0dbd8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="0dbd8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="0dbd8-161">c.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-161">c.</span></span> <span data-ttu-id="0dbd8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="0dbd8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0dbd8-163">The preceding values are not real values.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-163">The preceding values are not real values.</span></span> <span data-ttu-id="0dbd8-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

1. <span data-ttu-id="0dbd8-165">Tableau Server application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0dbd8-166">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-166">Configure the following claims for this application.</span></span> <span data-ttu-id="0dbd8-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="0dbd8-168">The following screenshot shows an example for the same.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-168">The following screenshot shows an example for the same.</span></span>
    
    ![Configure Single Sign-On](./media/tableauserver-tutorial/3.png)
    
1. <span data-ttu-id="0dbd8-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="0dbd8-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="0dbd8-171">Attribute Name</span></span> | <span data-ttu-id="0dbd8-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="0dbd8-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="0dbd8-173">username</span><span class="sxs-lookup"><span data-stu-id="0dbd8-173">username</span></span> | <span data-ttu-id="0dbd8-174">*user.mailnickname*</span><span class="sxs-lookup"><span data-stu-id="0dbd8-174">*user.mailnickname*</span></span> |

    <span data-ttu-id="0dbd8-175">a.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-175">a.</span></span> <span data-ttu-id="0dbd8-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="0dbd8-179">b.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-179">b.</span></span> <span data-ttu-id="0dbd8-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0dbd8-181">c.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-181">c.</span></span> <span data-ttu-id="0dbd8-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0dbd8-183">d.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-183">d.</span></span> <span data-ttu-id="0dbd8-184">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="0dbd8-184">Click **Ok**</span></span>


1. <span data-ttu-id="0dbd8-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

1. <span data-ttu-id="0dbd8-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-187">Click **Save** button.</span></span>

    <span data-ttu-id="0dbd8-188">![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="0dbd8-188">![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
1. <span data-ttu-id="0dbd8-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="0dbd8-190">a.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-190">a.</span></span> <span data-ttu-id="0dbd8-191">In the Tableau Server configuration, click the **SAML** tab.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="0dbd8-193">b.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-193">b.</span></span> <span data-ttu-id="0dbd8-194">Select the checkbox of **Use SAML for single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="0dbd8-195">c.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-195">c.</span></span> <span data-ttu-id="0dbd8-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="0dbd8-197">Using http://localhost is not recommended.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="0dbd8-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="0dbd8-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="0dbd8-200">d.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-200">d.</span></span> <span data-ttu-id="0dbd8-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="0dbd8-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="0dbd8-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="0dbd8-204">e.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-204">e.</span></span> <span data-ttu-id="0dbd8-205">Click the **Export Metadata File** and open it in the text editor application.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="0dbd8-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="0dbd8-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="0dbd8-208">f.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-208">f.</span></span> <span data-ttu-id="0dbd8-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="0dbd8-210">g.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-210">g.</span></span> <span data-ttu-id="0dbd8-211">Click the **OK** button in the Tableau Server Configuration page.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="0dbd8-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="0dbd8-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="0dbd8-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0dbd8-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0dbd8-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0dbd8-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dbd8-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dbd8-217">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0dbd8-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dbd8-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0dbd8-220">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0dbd8-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0dbd8-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tableauserver-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0dbd8-223">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/tableauserver-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0dbd8-225">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/tableauserver-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0dbd8-227">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0dbd8-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dbd8-229">a.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-229">a.</span></span> <span data-ttu-id="0dbd8-230">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dbd8-231">b.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-231">b.</span></span> <span data-ttu-id="0dbd8-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dbd8-233">c.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-233">c.</span></span> <span data-ttu-id="0dbd8-234">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0dbd8-235">d.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-235">d.</span></span> <span data-ttu-id="0dbd8-236">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="0dbd8-237">Creating a Tableau Server test user</span><span class="sxs-lookup"><span data-stu-id="0dbd8-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="0dbd8-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="0dbd8-239">You need to provision all the users in the Tableau server.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="0dbd8-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="0dbd8-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="0dbd8-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0dbd8-243">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0dbd8-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0dbd8-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Assign User][200] 

<span data-ttu-id="0dbd8-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0dbd8-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="0dbd8-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0dbd8-249">In the applications list, select **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-249">In the applications list, select **Tableau Server**.</span></span>

    ![Configure Single Sign-On](./media/tableauserver-tutorial/tutorial_tableauserver_app.png) 

1. <span data-ttu-id="0dbd8-251">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0dbd8-253">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-253">Click **Add** button.</span></span> <span data-ttu-id="0dbd8-254">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0dbd8-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0dbd8-257">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-257">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0dbd8-258">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dbd8-259">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0dbd8-259">Testing single sign-on</span></span>

<span data-ttu-id="0dbd8-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0dbd8-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span><span class="sxs-lookup"><span data-stu-id="0dbd8-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="0dbd8-262">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0dbd8-262">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0dbd8-263">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0dbd8-263">Additional resources</span></span>

* [<span data-ttu-id="0dbd8-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dbd8-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0dbd8-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dbd8-265">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/tableauserver-tutorial/tutorial_general_203.png

