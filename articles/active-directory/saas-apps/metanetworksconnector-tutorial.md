---
title: 'Tutorial: Azure Active Directory integration with Meta Networks Connector | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Meta Networks Connector.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4ae5f30d-113b-4261-b474-47ffbac08bf7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2018
ms.author: jeedes
ms.openlocfilehash: a3f40624e51ef287d70bed547eba7ec9e0882b0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866430"
---
# <a name="tutorial-azure-active-directory-integration-with-meta-networks-connector"></a><span data-ttu-id="4bff8-103">Tutorial: Azure Active Directory integration with Meta Networks Connector</span><span class="sxs-lookup"><span data-stu-id="4bff8-103">Tutorial: Azure Active Directory integration with Meta Networks Connector</span></span>

<span data-ttu-id="4bff8-104">In this tutorial, you learn how to integrate Meta Networks Connector with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bff8-104">In this tutorial, you learn how to integrate Meta Networks Connector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bff8-105">Integrating Meta Networks Connector with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4bff8-105">Integrating Meta Networks Connector with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4bff8-106">You can control in Azure AD who has access to Meta Networks Connector.</span><span class="sxs-lookup"><span data-stu-id="4bff8-106">You can control in Azure AD who has access to Meta Networks Connector.</span></span>
- <span data-ttu-id="4bff8-107">You can enable your users to automatically get signed-on to Meta Networks Connector (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4bff8-107">You can enable your users to automatically get signed-on to Meta Networks Connector (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4bff8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4bff8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4bff8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="4bff8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bff8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4bff8-110">Prerequisites</span></span>

<span data-ttu-id="4bff8-111">To configure Azure AD integration with Meta Networks Connector, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4bff8-111">To configure Azure AD integration with Meta Networks Connector, you need the following items:</span></span>

- <span data-ttu-id="4bff8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4bff8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bff8-113">A Meta Networks Connector single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4bff8-113">A Meta Networks Connector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bff8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4bff8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bff8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4bff8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bff8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4bff8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bff8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bff8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bff8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4bff8-118">Scenario description</span></span>
<span data-ttu-id="4bff8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4bff8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bff8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4bff8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bff8-121">Adding Meta Networks Connector from the gallery</span><span class="sxs-lookup"><span data-stu-id="4bff8-121">Adding Meta Networks Connector from the gallery</span></span>
1. <span data-ttu-id="4bff8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bff8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-meta-networks-connector-from-the-gallery"></a><span data-ttu-id="4bff8-123">Adding Meta Networks Connector from the gallery</span><span class="sxs-lookup"><span data-stu-id="4bff8-123">Adding Meta Networks Connector from the gallery</span></span>
<span data-ttu-id="4bff8-124">To configure the integration of Meta Networks Connector into Azure AD, you need to add Meta Networks Connector from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4bff8-124">To configure the integration of Meta Networks Connector into Azure AD, you need to add Meta Networks Connector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4bff8-125">**To add Meta Networks Connector from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bff8-125">**To add Meta Networks Connector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4bff8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4bff8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 
    
    ![The Azure Active Directory button][1]
    
1. <span data-ttu-id="4bff8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4bff8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-129">Then go to **All applications**.</span></span>
    
    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="4bff8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4bff8-131">To add new application, click **New application** button on the top of dialog.</span></span>
    
    ![The New application button][3]
    
1. <span data-ttu-id="4bff8-133">In the search box, type **Meta Networks Connector**, select **Meta Networks Connector** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4bff8-133">In the search box, type **Meta Networks Connector**, select **Meta Networks Connector** from result panel then click **Add** button to add the application.</span></span>
    
    ![Meta Networks Connector in the results list](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4bff8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bff8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4bff8-136">In this section, you configure and test Azure AD single sign-on with Meta Networks Connector based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4bff8-136">In this section, you configure and test Azure AD single sign-on with Meta Networks Connector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bff8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Meta Networks Connector is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bff8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Meta Networks Connector is to a user in Azure AD.</span></span> <span data-ttu-id="4bff8-138">In other words, a link relationship between an Azure AD user and the related user in Meta Networks Connector needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4bff8-138">In other words, a link relationship between an Azure AD user and the related user in Meta Networks Connector needs to be established.</span></span>

<span data-ttu-id="4bff8-139">To configure and test Azure AD single sign-on with Meta Networks Connector, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4bff8-139">To configure and test Azure AD single sign-on with Meta Networks Connector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4bff8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4bff8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4bff8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bff8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4bff8-142">**[Create a Meta Networks Connector test user](#create-a-meta-networks-connector-test-user)** - to have a counterpart of Britta Simon in Meta Networks Connector that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4bff8-142">**[Create a Meta Networks Connector test user](#create-a-meta-networks-connector-test-user)** - to have a counterpart of Britta Simon in Meta Networks Connector that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4bff8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bff8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4bff8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4bff8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4bff8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bff8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4bff8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Meta Networks Connector application.</span><span class="sxs-lookup"><span data-stu-id="4bff8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Meta Networks Connector application.</span></span>

<span data-ttu-id="4bff8-147">**To configure Azure AD single sign-on with Meta Networks Connector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bff8-147">**To configure Azure AD single sign-on with Meta Networks Connector, perform the following steps:**</span></span>

1. <span data-ttu-id="4bff8-148">In the Azure portal, on the **Meta Networks Connector** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-148">In the Azure portal, on the **Meta Networks Connector** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="4bff8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bff8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_samlbase.png)

1. <span data-ttu-id="4bff8-152">On the **Meta Networks Connector Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4bff8-152">On the **Meta Networks Connector Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Meta Networks Connector Domain and URLs single sign-on information](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_url.png)

    1. <span data-ttu-id="4bff8-154">In the **Identifier** textbox, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4bff8-154">In the **Identifier** textbox, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/saml/metadata`</span></span>
    
    1. <span data-ttu-id="4bff8-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="4bff8-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.nsof.io/v1/<ORGANIZATION-SHORT-NAME>/sso/saml`</span></span>
    
1. <span data-ttu-id="4bff8-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4bff8-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Meta Networks Connector Domain and URLs single sign-on information](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_url1.png)

    1. <span data-ttu-id="4bff8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/login`</span><span class="sxs-lookup"><span data-stu-id="4bff8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/login`</span></span>
    
    1. <span data-ttu-id="4bff8-159">In the **Relay State** textbox, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/#/`</span><span class="sxs-lookup"><span data-stu-id="4bff8-159">In the **Relay State** textbox, type a URL using the following pattern: `https://<ORGANIZATION-SHORT-NAME>.metanetworks.com/#/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4bff8-160">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4bff8-160">These values are not real.</span></span> <span data-ttu-id="4bff8-161">Update these values with the actual Identifier, Reply URL, and Sign-On URL are explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4bff8-161">Update these values with the actual Identifier, Reply URL, and Sign-On URL are explained later in the tutorial.</span></span>
    
1. <span data-ttu-id="4bff8-162">Meta Networks Connector application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="4bff8-162">Meta Networks Connector application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="4bff8-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="4bff8-163">Configure the following claims for this application.</span></span> <span data-ttu-id="4bff8-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="4bff8-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="4bff8-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="4bff8-165">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_attribute.png)
    
1. <span data-ttu-id="4bff8-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4bff8-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="4bff8-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="4bff8-168">Attribute Name</span></span> | <span data-ttu-id="4bff8-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="4bff8-169">Attribute Value</span></span> | <span data-ttu-id="4bff8-170">NAMESPACE</span><span class="sxs-lookup"><span data-stu-id="4bff8-170">NAMESPACE</span></span>|
    | ---------------| --------------- | -------- |
    | <span data-ttu-id="4bff8-171">firstname</span><span class="sxs-lookup"><span data-stu-id="4bff8-171">firstname</span></span> | <span data-ttu-id="4bff8-172">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4bff8-172">user.givenname</span></span> | |
    | <span data-ttu-id="4bff8-173">lastname</span><span class="sxs-lookup"><span data-stu-id="4bff8-173">lastname</span></span> | <span data-ttu-id="4bff8-174">user.surname</span><span class="sxs-lookup"><span data-stu-id="4bff8-174">user.surname</span></span> | |
    | <span data-ttu-id="4bff8-175">emailaddress</span><span class="sxs-lookup"><span data-stu-id="4bff8-175">emailaddress</span></span>| <span data-ttu-id="4bff8-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="4bff8-176">user.mail</span></span>| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
    | <span data-ttu-id="4bff8-177">name</span><span class="sxs-lookup"><span data-stu-id="4bff8-177">name</span></span> | <span data-ttu-id="4bff8-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4bff8-178">user.userprincipalname</span></span>| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
    | <span data-ttu-id="4bff8-179">phone</span><span class="sxs-lookup"><span data-stu-id="4bff8-179">phone</span></span> | <span data-ttu-id="4bff8-180">user.telephonenumber</span><span class="sxs-lookup"><span data-stu-id="4bff8-180">user.telephonenumber</span></span> | |

    1. <span data-ttu-id="4bff8-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bff8-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

        ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/tutorial_attribute_04.png)
    
        ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/tutorial_attribute_05.png)   
    
    1. <span data-ttu-id="4bff8-184">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4bff8-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    1. <span data-ttu-id="4bff8-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4bff8-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    1. <span data-ttu-id="4bff8-186">In the **Namespace** textbox, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4bff8-186">In the **Namespace** textbox, type the namespace value shown for that row.</span></span>
    
    1. <span data-ttu-id="4bff8-187">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="4bff8-187">Click **Ok**</span></span>
    
1. <span data-ttu-id="4bff8-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4bff8-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![The Certificate download link](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_certificate.png)
    
1. <span data-ttu-id="4bff8-190">On the **Meta Networks Connector Configuration** section, click **Configure Meta Networks Connector** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4bff8-190">On the **Meta Networks Connector Configuration** section, click **Configure Meta Networks Connector** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4bff8-191">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4bff8-191">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_configure.png)
    
1. <span data-ttu-id="4bff8-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4bff8-193">Click **Save** button.</span></span>
    
    ![Configure Single Sign-On Save button](./media/metanetworksconnector-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="4bff8-195">Open a new tab in your browser and log in to your Meta Networks Connector administrator account.</span><span class="sxs-lookup"><span data-stu-id="4bff8-195">Open a new tab in your browser and log in to your Meta Networks Connector administrator account.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4bff8-196">Meta Networks Connector is a secure system.</span><span class="sxs-lookup"><span data-stu-id="4bff8-196">Meta Networks Connector is a secure system.</span></span> <span data-ttu-id="4bff8-197">So before accessing their portal you need to get your public IP address whitelisted on their side.</span><span class="sxs-lookup"><span data-stu-id="4bff8-197">So before accessing their portal you need to get your public IP address whitelisted on their side.</span></span> <span data-ttu-id="4bff8-198">To get your public IP address,follow the below link specified [here](https://whatismyipaddress.com/).</span><span class="sxs-lookup"><span data-stu-id="4bff8-198">To get your public IP address,follow the below link specified [here](https://whatismyipaddress.com/).</span></span> <span data-ttu-id="4bff8-199">Send your IP address to the [Meta Networks Connector Client support team](mailto:support@metanetworks.com) to get your IP address whitelisted.</span><span class="sxs-lookup"><span data-stu-id="4bff8-199">Send your IP address to the [Meta Networks Connector Client support team](mailto:support@metanetworks.com) to get your IP address whitelisted.</span></span>
    
1. <span data-ttu-id="4bff8-200">Go to **Administrator** and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-200">Go to **Administrator** and select **Settings**.</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/configure3.png)
    
1. <span data-ttu-id="4bff8-202">Make sure **Log Internet Traffic** and **Force VPN MFA** are set to off.</span><span class="sxs-lookup"><span data-stu-id="4bff8-202">Make sure **Log Internet Traffic** and **Force VPN MFA** are set to off.</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/configure1.png)
    
1. <span data-ttu-id="4bff8-204">Go to **Administrator** and select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-204">Go to **Administrator** and select **SAML**.</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/configure4.png)
    
1. <span data-ttu-id="4bff8-206">Perform the following steps on the **DETAILS** page:</span><span class="sxs-lookup"><span data-stu-id="4bff8-206">Perform the following steps on the **DETAILS** page:</span></span>
    
    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/configure2.png)
    
    1. <span data-ttu-id="4bff8-208">Copy **SSO URL** value and paste it into the **Sign-In URL** textbox in the **Meta Networks Connector Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="4bff8-208">Copy **SSO URL** value and paste it into the **Sign-In URL** textbox in the **Meta Networks Connector Domain and URLs** section.</span></span>
    
    1. <span data-ttu-id="4bff8-209">Copy **Recipient URL** value and paste it into the **Reply URL** textbox in the **Meta Networks Connector Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="4bff8-209">Copy **Recipient URL** value and paste it into the **Reply URL** textbox in the **Meta Networks Connector Domain and URLs** section.</span></span>
    
    1. <span data-ttu-id="4bff8-210">Copy **Audience URI (SP Entity ID)** value and paste it into the **Identifier (Entity ID)** textbox in the **Meta Networks Connector Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="4bff8-210">Copy **Audience URI (SP Entity ID)** value and paste it into the **Identifier (Entity ID)** textbox in the **Meta Networks Connector Domain and URLs** section.</span></span>
    
    1. <span data-ttu-id="4bff8-211">Enable the SAML</span><span class="sxs-lookup"><span data-stu-id="4bff8-211">Enable the SAML</span></span>
    
1. <span data-ttu-id="4bff8-212">On the **GENERAL** tab. perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4bff8-212">On the **GENERAL** tab. perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/metanetworksconnector-tutorial/configure5.png)

    1. <span data-ttu-id="4bff8-214">In the **Identity Provider Single Sign-On URL**, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4bff8-214">In the **Identity Provider Single Sign-On URL**, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span></span>

    1. <span data-ttu-id="4bff8-215">In the **Identity Provider Issuer**, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4bff8-215">In the **Identity Provider Issuer**, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span></span>

    1. <span data-ttu-id="4bff8-216">Open the downloaded certificate from Azure portal in notepad, paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="4bff8-216">Open the downloaded certificate from Azure portal in notepad, paste it into the **X.509 Certificate** textbox.</span></span>

    1. <span data-ttu-id="4bff8-217">Enable the **Just-in-Time Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-217">Enable the **Just-in-Time Provisioning**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4bff8-218">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4bff8-218">Create an Azure AD test user</span></span>

<span data-ttu-id="4bff8-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bff8-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>
    
![Create an Azure AD test user][100]
    
<span data-ttu-id="4bff8-221">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bff8-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4bff8-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4bff8-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>
    
    ![The Azure Active Directory button](./media/metanetworksconnector-tutorial/create_aaduser_01.png)
    
1. <span data-ttu-id="4bff8-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/metanetworksconnector-tutorial/create_aaduser_02.png)
    
1. <span data-ttu-id="4bff8-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4bff8-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
    
    ![The Add button](./media/metanetworksconnector-tutorial/create_aaduser_03.png)
    
1. <span data-ttu-id="4bff8-228">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4bff8-228">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/metanetworksconnector-tutorial/create_aaduser_04.png)
    
    1. <span data-ttu-id="4bff8-230">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-230">In the **Name** box, type **BrittaSimon**.</span></span>

    1. <span data-ttu-id="4bff8-231">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bff8-231">In the **User name** box, type the email address of user Britta Simon.</span></span>
    
    1. <span data-ttu-id="4bff8-232">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4bff8-232">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>
    
    1. <span data-ttu-id="4bff8-233">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-233">Click **Create**.</span></span>
    
### <a name="create-a-meta-networks-connector-test-user"></a><span data-ttu-id="4bff8-234">Create a Meta Networks Connector test user</span><span class="sxs-lookup"><span data-stu-id="4bff8-234">Create a Meta Networks Connector test user</span></span>

<span data-ttu-id="4bff8-235">The objective of this section is to create a user called Britta Simon in Meta Networks Connector.</span><span class="sxs-lookup"><span data-stu-id="4bff8-235">The objective of this section is to create a user called Britta Simon in Meta Networks Connector.</span></span> <span data-ttu-id="4bff8-236">Meta Networks Connector supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="4bff8-236">Meta Networks Connector supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4bff8-237">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="4bff8-237">There is no action item for you in this section.</span></span> <span data-ttu-id="4bff8-238">A new user is created during an attempt to access Meta Networks Connector if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="4bff8-238">A new user is created during an attempt to access Meta Networks Connector if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="4bff8-239">If you need to create a user manually, contact [Meta Networks Connector Client support team](mailto:support@metanetworks.com).</span><span class="sxs-lookup"><span data-stu-id="4bff8-239">If you need to create a user manually, contact [Meta Networks Connector Client support team](mailto:support@metanetworks.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4bff8-240">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4bff8-240">Assign the Azure AD test user</span></span>

<span data-ttu-id="4bff8-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Meta Networks Connector.</span><span class="sxs-lookup"><span data-stu-id="4bff8-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Meta Networks Connector.</span></span>

![Assign the user role][200]

<span data-ttu-id="4bff8-243">**To assign Britta Simon to Meta Networks Connector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bff8-243">**To assign Britta Simon to Meta Networks Connector, perform the following steps:**</span></span>

1. <span data-ttu-id="4bff8-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>
    
    ![Assign User][201]
    
1. <span data-ttu-id="4bff8-246">In the applications list, select **Meta Networks Connector**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-246">In the applications list, select **Meta Networks Connector**.</span></span>
    
    ![The Meta Networks Connector link in the Applications list](./media/metanetworksconnector-tutorial/tutorial_metanetworksconnector_app.png)  
    
1. <span data-ttu-id="4bff8-248">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4bff8-248">In the menu on the left, click **Users and groups**.</span></span>
    
    ![The "Users and groups" link][202]
    
1. <span data-ttu-id="4bff8-250">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4bff8-250">Click **Add** button.</span></span> <span data-ttu-id="4bff8-251">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bff8-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>
    
    ![The Add Assignment pane][203]
    
1. <span data-ttu-id="4bff8-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4bff8-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>
    
1. <span data-ttu-id="4bff8-254">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bff8-254">Click **Select** button on **Users and groups** dialog.</span></span>
    
1. <span data-ttu-id="4bff8-255">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bff8-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4bff8-256">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bff8-256">Test single sign-on</span></span>

<span data-ttu-id="4bff8-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4bff8-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4bff8-258">When you click the Meta Networks Connector tile in the Access Panel, you should get automatically signed-on to your Meta Networks Connector application.</span><span class="sxs-lookup"><span data-stu-id="4bff8-258">When you click the Meta Networks Connector tile in the Access Panel, you should get automatically signed-on to your Meta Networks Connector application.</span></span>
<span data-ttu-id="4bff8-259">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4bff8-259">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bff8-260">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4bff8-260">Additional resources</span></span>

- [<span data-ttu-id="4bff8-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bff8-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
- [<span data-ttu-id="4bff8-262">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4bff8-262">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/metanetworksconnector-tutorial/tutorial_general_01.png
[2]: ./media/metanetworksconnector-tutorial/tutorial_general_02.png
[3]: ./media/metanetworksconnector-tutorial/tutorial_general_03.png
[4]: ./media/metanetworksconnector-tutorial/tutorial_general_04.png

[100]: ./media/metanetworksconnector-tutorial/tutorial_general_100.png

[200]: ./media/metanetworksconnector-tutorial/tutorial_general_200.png
[201]: ./media/metanetworksconnector-tutorial/tutorial_general_201.png
[202]: ./media/metanetworksconnector-tutorial/tutorial_general_202.png
[203]: ./media/metanetworksconnector-tutorial/tutorial_general_203.png

