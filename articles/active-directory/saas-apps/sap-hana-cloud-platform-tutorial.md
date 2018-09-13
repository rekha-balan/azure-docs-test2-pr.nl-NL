---
title: 'Tutorial: Azure Active Directory integration with SAP Cloud Platform | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Cloud Platform.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/15/2017
ms.author: jeedes
ms.openlocfilehash: 07b3c32601d90fdeed1c335c0f36a5ccbdbe4f1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870401"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-platform"></a><span data-ttu-id="52cab-103">Tutorial: Azure Active Directory integration with SAP Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="52cab-103">Tutorial: Azure Active Directory integration with SAP Cloud Platform</span></span>

<span data-ttu-id="52cab-104">In this tutorial, you learn how to integrate SAP Cloud Platform with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52cab-104">In this tutorial, you learn how to integrate SAP Cloud Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52cab-105">Integrating SAP Cloud Platform with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="52cab-105">Integrating SAP Cloud Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52cab-106">You can control in Azure AD who has access to SAP Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="52cab-106">You can control in Azure AD who has access to SAP Cloud Platform.</span></span>
- <span data-ttu-id="52cab-107">You can enable your users to automatically get signed-on to SAP Cloud Platform (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="52cab-107">You can enable your users to automatically get signed-on to SAP Cloud Platform (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="52cab-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="52cab-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="52cab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="52cab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52cab-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52cab-110">Prerequisites</span></span>

<span data-ttu-id="52cab-111">To configure Azure AD integration with SAP Cloud Platform, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="52cab-111">To configure Azure AD integration with SAP Cloud Platform, you need the following items:</span></span>

- <span data-ttu-id="52cab-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="52cab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52cab-113">A SAP Cloud Platform single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="52cab-113">A SAP Cloud Platform single sign-on enabled subscription</span></span>

<span data-ttu-id="52cab-114">After completing this tutorial, the Azure AD users you have assigned to SAP Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52cab-114">After completing this tutorial, the Azure AD users you have assigned to SAP Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="52cab-115">You need to deploy your own application or subscribe to an application on your SAP Cloud Platform account to test single sign on.</span><span class="sxs-lookup"><span data-stu-id="52cab-115">You need to deploy your own application or subscribe to an application on your SAP Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="52cab-116">In this tutorial, an application is deployed in the account.</span><span class="sxs-lookup"><span data-stu-id="52cab-116">In this tutorial, an application is deployed in the account.</span></span>
> 

<span data-ttu-id="52cab-117">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="52cab-117">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52cab-118">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="52cab-118">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52cab-119">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52cab-119">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52cab-120">Scenario description</span><span class="sxs-lookup"><span data-stu-id="52cab-120">Scenario description</span></span>
<span data-ttu-id="52cab-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="52cab-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52cab-122">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="52cab-122">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52cab-123">Adding SAP Cloud Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="52cab-123">Adding SAP Cloud Platform from the gallery</span></span>
1. <span data-ttu-id="52cab-124">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52cab-124">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-platform-from-the-gallery"></a><span data-ttu-id="52cab-125">Adding SAP Cloud Platform from the gallery</span><span class="sxs-lookup"><span data-stu-id="52cab-125">Adding SAP Cloud Platform from the gallery</span></span>
<span data-ttu-id="52cab-126">To configure the integration of SAP Cloud Platform into Azure AD, you need to add SAP Cloud Platform from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="52cab-126">To configure the integration of SAP Cloud Platform into Azure AD, you need to add SAP Cloud Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52cab-127">**To add SAP Cloud Platform from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52cab-127">**To add SAP Cloud Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52cab-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="52cab-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="52cab-130">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="52cab-130">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52cab-131">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="52cab-131">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="52cab-133">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="52cab-133">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="52cab-135">In the search box, type **SAP Cloud Platform**, select **SAP Cloud Platform** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="52cab-135">In the search box, type **SAP Cloud Platform**, select **SAP Cloud Platform** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Cloud Platform in the results list](./media/sap-hana-cloud-platform-tutorial/tutorial_sapcloudplatform_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="52cab-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52cab-137">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="52cab-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud Platform based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52cab-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52cab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud Platform is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52cab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud Platform is to a user in Azure AD.</span></span> <span data-ttu-id="52cab-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud Platform needs to be established.</span><span class="sxs-lookup"><span data-stu-id="52cab-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud Platform needs to be established.</span></span>

<span data-ttu-id="52cab-141">In SAP Cloud Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="52cab-141">In SAP Cloud Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52cab-142">To configure and test Azure AD single sign-on with SAP Cloud Platform, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="52cab-142">To configure and test Azure AD single sign-on with SAP Cloud Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52cab-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="52cab-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="52cab-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52cab-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="52cab-145">**[Create a SAP Cloud Platform test user](#create-a-sap-cloud-platform-test-user)** - to have a counterpart of Britta Simon in SAP Cloud Platform that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="52cab-145">**[Create a SAP Cloud Platform test user](#create-a-sap-cloud-platform-test-user)** - to have a counterpart of Britta Simon in SAP Cloud Platform that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="52cab-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="52cab-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="52cab-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="52cab-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="52cab-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52cab-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="52cab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud Platform application.</span><span class="sxs-lookup"><span data-stu-id="52cab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud Platform application.</span></span>

<span data-ttu-id="52cab-150">**To configure Azure AD single sign-on with SAP Cloud Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52cab-150">**To configure Azure AD single sign-on with SAP Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="52cab-151">In the Azure portal, on the **SAP Cloud Platform** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="52cab-151">In the Azure portal, on the **SAP Cloud Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="52cab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="52cab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sap-hana-cloud-platform-tutorial/tutorial_sapcloudplatform_samlbase.png)

1. <span data-ttu-id="52cab-155">On the **SAP Cloud Platform Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52cab-155">On the **SAP Cloud Platform Domain and URLs** section, perform the following steps:</span></span>

    ![SAP Cloud Platform Domain and URLs single sign-on information](./media/sap-hana-cloud-platform-tutorial/tutorial_sapcloudplatform_url.png)

    <span data-ttu-id="52cab-157">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-157">a.</span></span> <span data-ttu-id="52cab-158">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP Cloud Platform** application.</span><span class="sxs-lookup"><span data-stu-id="52cab-158">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP Cloud Platform** application.</span></span> <span data-ttu-id="52cab-159">This is the account-specific URL of a protected resource in your SAP Cloud Platform application.</span><span class="sxs-lookup"><span data-stu-id="52cab-159">This is the account-specific URL of a protected resource in your SAP Cloud Platform application.</span></span> <span data-ttu-id="52cab-160">The URL is based on the following pattern: `https://<applicationName><accountName>.<landscape host>.ondemand.com/<path_to_protected_resource>`</span><span class="sxs-lookup"><span data-stu-id="52cab-160">The URL is based on the following pattern: `https://<applicationName><accountName>.<landscape host>.ondemand.com/<path_to_protected_resource>`</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="52cab-161">This is the URL in your SAP Cloud Platform application that requires the user to authenticate.</span><span class="sxs-lookup"><span data-stu-id="52cab-161">This is the URL in your SAP Cloud Platform application that requires the user to authenticate.</span></span>
     > 

    | |
    |--|
    | `https://<subdomain>.hanatrial.ondemand.com/<instancename>` |
    | `https://<subdomain>.hana.ondemand.com/<instancename>` |

    <span data-ttu-id="52cab-162">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-162">b.</span></span> <span data-ttu-id="52cab-163">In the **Identifier** textbox you will provide your SAP Cloud Platform's type a URL using one of the following patterns:</span><span class="sxs-lookup"><span data-stu-id="52cab-163">In the **Identifier** textbox you will provide your SAP Cloud Platform's type a URL using one of the following patterns:</span></span> 

    | |
    |--|
    | `https://hanatrial.ondemand.com/<instancename>` |
    | `https://hana.ondemand.com/<instancename>` |
    | `https://us1.hana.ondemand.com/<instancename>` |
    | `https://ap1.hana.ondemand.com/<instancename>` |

    <span data-ttu-id="52cab-164">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-164">c.</span></span> <span data-ttu-id="52cab-165">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="52cab-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    | |
    |--|
    | `https://<subdomain>.hanatrial.ondemand.com/<instancename>` |
    | `https://<subdomain>.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.us1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.us1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.ap1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.ap1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.hana.ondemand.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="52cab-166">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="52cab-166">These values are not real.</span></span> <span data-ttu-id="52cab-167">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="52cab-167">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span></span> <span data-ttu-id="52cab-168">Contact [SAP Cloud Platform Client support team](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/5dd739823b824b539eee47b7860a00be.html) to get Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="52cab-168">Contact [SAP Cloud Platform Client support team](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/5dd739823b824b539eee47b7860a00be.html) to get Sign-On URL and Identifier.</span></span> <span data-ttu-id="52cab-169">Reply URL you can get from trust management section which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="52cab-169">Reply URL you can get from trust management section which is explained later in the tutorial.</span></span>
    > 
     
1. <span data-ttu-id="52cab-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="52cab-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/sap-hana-cloud-platform-tutorial/tutorial_sapcloudplatform_certificate.png) 

1. <span data-ttu-id="52cab-172">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="52cab-172">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sap-hana-cloud-platform-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="52cab-174">In a different web browser window, sign on to the SAP Cloud Platform Cockpit at `https://account.<landscape host>.ondemand.com/cockpit`(for example: https://account.hanatrial.ondemand.com/cockpit).</span><span class="sxs-lookup"><span data-stu-id="52cab-174">In a different web browser window, sign on to the SAP Cloud Platform Cockpit at `https://account.<landscape host>.ondemand.com/cockpit`(for example: https://account.hanatrial.ondemand.com/cockpit).</span></span>

1. <span data-ttu-id="52cab-175">Click the **Trust** tab.</span><span class="sxs-lookup"><span data-stu-id="52cab-175">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="52cab-176">![Trust](./media/sap-hana-cloud-platform-tutorial/ic790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="52cab-176">![Trust](./media/sap-hana-cloud-platform-tutorial/ic790800.png "Trust")</span></span>

1. <span data-ttu-id="52cab-177">In the Trust Management section, under **Local Service Provider**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52cab-177">In the Trust Management section, under **Local Service Provider**, perform the following steps:</span></span>

    <span data-ttu-id="52cab-178">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic793931.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="52cab-178">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic793931.png "Trust Management")</span></span>
   
    <span data-ttu-id="52cab-179">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-179">a.</span></span> <span data-ttu-id="52cab-180">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="52cab-180">Click **Edit**.</span></span>

    <span data-ttu-id="52cab-181">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-181">b.</span></span> <span data-ttu-id="52cab-182">As **Configuration Type**, select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="52cab-182">As **Configuration Type**, select **Custom**.</span></span>

    <span data-ttu-id="52cab-183">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-183">c.</span></span> <span data-ttu-id="52cab-184">As **Local Provider Name**, leave the default value.</span><span class="sxs-lookup"><span data-stu-id="52cab-184">As **Local Provider Name**, leave the default value.</span></span> <span data-ttu-id="52cab-185">Copy this value and paste it into the **Identifier** field in the Azure AD configuration for SAP Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="52cab-185">Copy this value and paste it into the **Identifier** field in the Azure AD configuration for SAP Cloud Platform.</span></span>

    <span data-ttu-id="52cab-186">d.</span><span class="sxs-lookup"><span data-stu-id="52cab-186">d.</span></span> <span data-ttu-id="52cab-187">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="52cab-187">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>

    <span data-ttu-id="52cab-188">e.</span><span class="sxs-lookup"><span data-stu-id="52cab-188">e.</span></span> <span data-ttu-id="52cab-189">As **Principal Propagation**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="52cab-189">As **Principal Propagation**, select **Disabled**.</span></span>

    <span data-ttu-id="52cab-190">f.</span><span class="sxs-lookup"><span data-stu-id="52cab-190">f.</span></span> <span data-ttu-id="52cab-191">As **Force Authentication**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="52cab-191">As **Force Authentication**, select **Disabled**.</span></span>

    <span data-ttu-id="52cab-192">g.</span><span class="sxs-lookup"><span data-stu-id="52cab-192">g.</span></span> <span data-ttu-id="52cab-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="52cab-193">Click **Save**.</span></span>

1. <span data-ttu-id="52cab-194">After saving the **Local Service Provider** settings, perform the following to obtain the Reply URL:</span><span class="sxs-lookup"><span data-stu-id="52cab-194">After saving the **Local Service Provider** settings, perform the following to obtain the Reply URL:</span></span>
   
    <span data-ttu-id="52cab-195">![Get Metadata](./media/sap-hana-cloud-platform-tutorial/ic793930.png "Get Metadata")</span><span class="sxs-lookup"><span data-stu-id="52cab-195">![Get Metadata](./media/sap-hana-cloud-platform-tutorial/ic793930.png "Get Metadata")</span></span>

    <span data-ttu-id="52cab-196">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-196">a.</span></span> <span data-ttu-id="52cab-197">Download the SAP Cloud Platform metadata file by clicking **Get Metadata**.</span><span class="sxs-lookup"><span data-stu-id="52cab-197">Download the SAP Cloud Platform metadata file by clicking **Get Metadata**.</span></span>

    <span data-ttu-id="52cab-198">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-198">b.</span></span> <span data-ttu-id="52cab-199">Open the downloaded SAP Cloud Platform metadata XML file, and then locate the **ns3:AssertionConsumerService** tag.</span><span class="sxs-lookup"><span data-stu-id="52cab-199">Open the downloaded SAP Cloud Platform metadata XML file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
 
    <span data-ttu-id="52cab-200">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-200">c.</span></span> <span data-ttu-id="52cab-201">Copy the value of the **Location** attribute, and then paste it into the **Reply URL** field in the Azure AD configuration for SAP Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="52cab-201">Copy the value of the **Location** attribute, and then paste it into the **Reply URL** field in the Azure AD configuration for SAP Cloud Platform.</span></span>

1. <span data-ttu-id="52cab-202">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="52cab-202">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="52cab-203">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic790802.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="52cab-203">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="52cab-204">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span><span class="sxs-lookup"><span data-stu-id="52cab-204">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="52cab-205">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="52cab-205">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="52cab-206">For None, you don't have any trust settings.</span><span class="sxs-lookup"><span data-stu-id="52cab-206">For None, you don't have any trust settings.</span></span>
    > 
    > 

1. <span data-ttu-id="52cab-207">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="52cab-207">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="52cab-208">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic793932.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="52cab-208">![Trust Management](./media/sap-hana-cloud-platform-tutorial/ic793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="52cab-209">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL**, and **Signing Certificate** are populated automatically.</span><span class="sxs-lookup"><span data-stu-id="52cab-209">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL**, and **Signing Certificate** are populated automatically.</span></span>
    > 
     
1. <span data-ttu-id="52cab-210">Click the **Attributes** tab.</span><span class="sxs-lookup"><span data-stu-id="52cab-210">Click the **Attributes** tab.</span></span>

1. <span data-ttu-id="52cab-211">On the **Attributes** tab, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="52cab-211">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="52cab-212">![Attributes](./media/sap-hana-cloud-platform-tutorial/ic790804.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="52cab-212">![Attributes](./media/sap-hana-cloud-platform-tutorial/ic790804.png "Attributes")</span></span> 

    <span data-ttu-id="52cab-213">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-213">a.</span></span> <span data-ttu-id="52cab-214">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span><span class="sxs-lookup"><span data-stu-id="52cab-214">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="52cab-215">Assertion Attribute</span><span class="sxs-lookup"><span data-stu-id="52cab-215">Assertion Attribute</span></span> | <span data-ttu-id="52cab-216">Principal Attribute</span><span class="sxs-lookup"><span data-stu-id="52cab-216">Principal Attribute</span></span> |
    | --- | --- |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` |<span data-ttu-id="52cab-217">firstname</span><span class="sxs-lookup"><span data-stu-id="52cab-217">firstname</span></span> |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` |<span data-ttu-id="52cab-218">lastname</span><span class="sxs-lookup"><span data-stu-id="52cab-218">lastname</span></span> |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |<span data-ttu-id="52cab-219">email</span><span class="sxs-lookup"><span data-stu-id="52cab-219">email</span></span> |
   
     >[!NOTE]
     ><span data-ttu-id="52cab-220">The configuration of the Attributes depends on how the application(s) on SCP are developed, that is, which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span><span class="sxs-lookup"><span data-stu-id="52cab-220">The configuration of the Attributes depends on how the application(s) on SCP are developed, that is, which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
    
    <span data-ttu-id="52cab-221">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-221">b.</span></span> <span data-ttu-id="52cab-222">The **Default Attribute** in the screenshot is just for illustration purposes.</span><span class="sxs-lookup"><span data-stu-id="52cab-222">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="52cab-223">It is not required to make the scenario work.</span><span class="sxs-lookup"><span data-stu-id="52cab-223">It is not required to make the scenario work.</span></span>  
 
    <span data-ttu-id="52cab-224">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-224">c.</span></span> <span data-ttu-id="52cab-225">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span><span class="sxs-lookup"><span data-stu-id="52cab-225">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="52cab-226">It is possible that your application requires different mappings.</span><span class="sxs-lookup"><span data-stu-id="52cab-226">It is possible that your application requires different mappings.</span></span>

### <a name="assertion-based-groups"></a><span data-ttu-id="52cab-227">Assertion-based groups</span><span class="sxs-lookup"><span data-stu-id="52cab-227">Assertion-based groups</span></span>

<span data-ttu-id="52cab-228">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="52cab-228">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="52cab-229">Using groups on SAP Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span><span class="sxs-lookup"><span data-stu-id="52cab-229">Using groups on SAP Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="52cab-230">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span><span class="sxs-lookup"><span data-stu-id="52cab-230">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="52cab-231">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP Cloud Platform account.</span><span class="sxs-lookup"><span data-stu-id="52cab-231">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP Cloud Platform account.</span></span>
 
<span data-ttu-id="52cab-232">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP Cloud Platform account.</span><span class="sxs-lookup"><span data-stu-id="52cab-232">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP Cloud Platform account.</span></span> <span data-ttu-id="52cab-233">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP Cloud Platform cockpit.</span><span class="sxs-lookup"><span data-stu-id="52cab-233">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP Cloud Platform cockpit.</span></span>

> [!TIP]
> <span data-ttu-id="52cab-234">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="52cab-234">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52cab-235">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="52cab-235">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52cab-236">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52cab-236">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="52cab-237">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="52cab-237">Create an Azure AD test user</span></span>

<span data-ttu-id="52cab-238">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52cab-238">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="52cab-240">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52cab-240">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52cab-241">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="52cab-241">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sap-hana-cloud-platform-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="52cab-243">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="52cab-243">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sap-hana-cloud-platform-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="52cab-245">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="52cab-245">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sap-hana-cloud-platform-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="52cab-247">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52cab-247">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sap-hana-cloud-platform-tutorial/create_aaduser_04.png)

    <span data-ttu-id="52cab-249">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-249">a.</span></span> <span data-ttu-id="52cab-250">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52cab-250">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52cab-251">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-251">b.</span></span> <span data-ttu-id="52cab-252">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52cab-252">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="52cab-253">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-253">c.</span></span> <span data-ttu-id="52cab-254">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="52cab-254">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="52cab-255">d.</span><span class="sxs-lookup"><span data-stu-id="52cab-255">d.</span></span> <span data-ttu-id="52cab-256">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="52cab-256">Click **Create**.</span></span>
 
### <a name="create-a-sap-cloud-platform-test-user"></a><span data-ttu-id="52cab-257">Create a SAP Cloud Platform test user</span><span class="sxs-lookup"><span data-stu-id="52cab-257">Create a SAP Cloud Platform test user</span></span>

<span data-ttu-id="52cab-258">In order to enable Azure AD users to log in to SAP Cloud Platform, you must assign roles in the SAP Cloud Platform to them.</span><span class="sxs-lookup"><span data-stu-id="52cab-258">In order to enable Azure AD users to log in to SAP Cloud Platform, you must assign roles in the SAP Cloud Platform to them.</span></span>

<span data-ttu-id="52cab-259">**To assign a role to a user, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52cab-259">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="52cab-260">Log in to your **SAP Cloud Platform** cockpit.</span><span class="sxs-lookup"><span data-stu-id="52cab-260">Log in to your **SAP Cloud Platform** cockpit.</span></span>

1. <span data-ttu-id="52cab-261">Perform the following:</span><span class="sxs-lookup"><span data-stu-id="52cab-261">Perform the following:</span></span>
   
    <span data-ttu-id="52cab-262">![Authorizations](./media/sap-hana-cloud-platform-tutorial/ic790805.png "Authorizations")</span><span class="sxs-lookup"><span data-stu-id="52cab-262">![Authorizations](./media/sap-hana-cloud-platform-tutorial/ic790805.png "Authorizations")</span></span>
   
    <span data-ttu-id="52cab-263">a.</span><span class="sxs-lookup"><span data-stu-id="52cab-263">a.</span></span> <span data-ttu-id="52cab-264">Click **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="52cab-264">Click **Authorization**.</span></span>

    <span data-ttu-id="52cab-265">b.</span><span class="sxs-lookup"><span data-stu-id="52cab-265">b.</span></span> <span data-ttu-id="52cab-266">Click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="52cab-266">Click the **Users** tab.</span></span>

    <span data-ttu-id="52cab-267">c.</span><span class="sxs-lookup"><span data-stu-id="52cab-267">c.</span></span> <span data-ttu-id="52cab-268">In the **User** textbox, type the user’s email address.</span><span class="sxs-lookup"><span data-stu-id="52cab-268">In the **User** textbox, type the user’s email address.</span></span>

    <span data-ttu-id="52cab-269">d.</span><span class="sxs-lookup"><span data-stu-id="52cab-269">d.</span></span> <span data-ttu-id="52cab-270">Click **Assign** to assign the user to a role.</span><span class="sxs-lookup"><span data-stu-id="52cab-270">Click **Assign** to assign the user to a role.</span></span>

    <span data-ttu-id="52cab-271">e.</span><span class="sxs-lookup"><span data-stu-id="52cab-271">e.</span></span> <span data-ttu-id="52cab-272">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="52cab-272">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="52cab-273">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="52cab-273">Assign the Azure AD test user</span></span>

<span data-ttu-id="52cab-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="52cab-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud Platform.</span></span>

![Assign the user role][200] 

<span data-ttu-id="52cab-276">**To assign Britta Simon to SAP Cloud Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52cab-276">**To assign Britta Simon to SAP Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="52cab-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="52cab-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="52cab-279">In the applications list, select **SAP Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="52cab-279">In the applications list, select **SAP Cloud Platform**.</span></span>

    ![The SAP Cloud Platform link in the Applications list](./media/sap-hana-cloud-platform-tutorial/tutorial_sapcloudplatform_app.png)  

1. <span data-ttu-id="52cab-281">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="52cab-281">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="52cab-283">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="52cab-283">Click **Add** button.</span></span> <span data-ttu-id="52cab-284">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="52cab-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="52cab-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="52cab-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="52cab-287">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="52cab-287">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="52cab-288">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="52cab-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="52cab-289">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="52cab-289">Test single sign-on</span></span>

<span data-ttu-id="52cab-290">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="52cab-290">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52cab-291">When you click the SAP Cloud Platform tile in the Access Panel, you should get automatically signed-on to your SAP Cloud Platform application.</span><span class="sxs-lookup"><span data-stu-id="52cab-291">When you click the SAP Cloud Platform tile in the Access Panel, you should get automatically signed-on to your SAP Cloud Platform application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="52cab-292">Additional resources</span><span class="sxs-lookup"><span data-stu-id="52cab-292">Additional resources</span></span>

* [<span data-ttu-id="52cab-293">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52cab-293">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="52cab-294">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52cab-294">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_01.png
[2]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_02.png
[3]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_03.png
[4]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_04.png

[100]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_100.png

[200]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_200.png
[201]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_201.png
[202]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_202.png
[203]: ./media/sap-hana-cloud-platform-tutorial/tutorial_general_203.png

