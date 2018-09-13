---
title: 'Tutorial: Azure Active Directory integration with SAP HANA | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP HANA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: e498b0ca4b9efe09c2fe2f2bfcdcb3cc68b9c2c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867574"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="dc4d5-103">Tutorial: Azure Active Directory integration with SAP HANA</span><span class="sxs-lookup"><span data-stu-id="dc4d5-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="dc4d5-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc4d5-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc4d5-105">When you integrate SAP HANA with Azure AD, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-105">When you integrate SAP HANA with Azure AD, you get the following benefits:</span></span>

- <span data-ttu-id="dc4d5-106">You can control in Azure AD who has access to SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-106">You can control in Azure AD who has access to SAP HANA.</span></span>
- <span data-ttu-id="dc4d5-107">You can enable your users to automatically get signed into SAP HANA with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-107">You can enable your users to automatically get signed into SAP HANA with their Azure AD accounts.</span></span>
- <span data-ttu-id="dc4d5-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="dc4d5-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dc4d5-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc4d5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc4d5-110">Prerequisites</span></span>

<span data-ttu-id="dc4d5-111">To configure Azure AD integration with SAP HANA, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="dc4d5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dc4d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc4d5-113">A SAP HANA subscription that's single sign-on (SSO) enabled</span><span class="sxs-lookup"><span data-stu-id="dc4d5-113">A SAP HANA subscription that's single sign-on (SSO) enabled</span></span>
- <span data-ttu-id="dc4d5-114">A HANA instance that's running on any public IaaS, on-premises, Azure VM, or SAP large instances in Azure</span><span class="sxs-lookup"><span data-stu-id="dc4d5-114">A HANA instance that's running on any public IaaS, on-premises, Azure VM, or SAP large instances in Azure</span></span>
- <span data-ttu-id="dc4d5-115">The XSA Administration web interface, as well as HANA Studio installed on the HANA instance</span><span class="sxs-lookup"><span data-stu-id="dc4d5-115">The XSA Administration web interface, as well as HANA Studio installed on the HANA instance</span></span>

> [!NOTE]
> <span data-ttu-id="dc4d5-116">We do not recommend using a production environment of SAP HANA to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-116">We do not recommend using a production environment of SAP HANA to test the steps in this tutorial.</span></span> <span data-ttu-id="dc4d5-117">Test the integration first in the development or staging environment of the application, and then use the production environment.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-117">Test the integration first in the development or staging environment of the application, and then use the production environment.</span></span>

<span data-ttu-id="dc4d5-118">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-118">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="dc4d5-119">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-119">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="dc4d5-120">[Get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/) of Azure AD if you don't already have an Azure AD trial environment.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-120">[Get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/) of Azure AD if you don't already have an Azure AD trial environment.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc4d5-121">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dc4d5-121">Scenario description</span></span>
<span data-ttu-id="dc4d5-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc4d5-123">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-123">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc4d5-124">Adding SAP HANA from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc4d5-124">Adding SAP HANA from the gallery</span></span>
1. <span data-ttu-id="dc4d5-125">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc4d5-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-sap-hana-from-the-gallery"></a><span data-ttu-id="dc4d5-126">Add SAP HANA from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc4d5-126">Add SAP HANA from the gallery</span></span>
<span data-ttu-id="dc4d5-127">To configure the integration of SAP HANA into Azure AD, add SAP HANA from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-127">To configure the integration of SAP HANA into Azure AD, add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc4d5-128">**To add SAP HANA from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc4d5-128">**To add SAP HANA from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="dc4d5-129">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-129">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="dc4d5-131">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-131">Go to **Enterprise applications**.</span></span> <span data-ttu-id="dc4d5-132">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-132">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="dc4d5-134">To add the new application, select the **New application** button on the top of dialog box.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-134">To add the new application, select the **New application** button on the top of dialog box.</span></span>

    ![The new application button][3]

1. <span data-ttu-id="dc4d5-136">In the search box, type **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-136">In the search box, type **SAP HANA**.</span></span> <span data-ttu-id="dc4d5-137">Then select **SAP HANA** from the results panel.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-137">Then select **SAP HANA** from the results panel.</span></span> <span data-ttu-id="dc4d5-138">Finally, select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-138">Finally, select the **Add** button to add the application.</span></span> 

    ![The new application](./media/saphana-tutorial/tutorial_saphana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dc4d5-140">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc4d5-140">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="dc4d5-141">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dc4d5-141">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dc4d5-142">For single sign-on to work, Azure AD needs to know who the counterpart user in SAP HANA is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-142">For single sign-on to work, Azure AD needs to know who the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="dc4d5-143">In other words, you need to establish a link  between an Azure AD user and the related user in SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-143">In other words, you need to establish a link  between an Azure AD user and the related user in SAP HANA.</span></span>

<span data-ttu-id="dc4d5-144">In SAP HANA, give the **Username** value the same value of the **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-144">In SAP HANA, give the **Username** value the same value of the **user name** in Azure AD.</span></span> <span data-ttu-id="dc4d5-145">This step establishes the link between the two users.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-145">This step establishes the link between the two users.</span></span>

<span data-ttu-id="dc4d5-146">To configure and test Azure AD single sign-on with SAP HANA, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-146">To configure and test Azure AD single sign-on with SAP HANA, complete the following building blocks:</span></span>

1. <span data-ttu-id="dc4d5-147">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-147">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dc4d5-148">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-148">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dc4d5-149">[Create a SAP HANA test user](#creating-a-sap-hana-test-user) to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-149">[Create a SAP HANA test user](#creating-a-sap-hana-test-user) to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of the user.</span></span>
1. <span data-ttu-id="dc4d5-150">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-150">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dc4d5-151">[Test single sign-on](#testing-single-sign-on) to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-151">[Test single sign-on](#testing-single-sign-on) to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dc4d5-152">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc4d5-152">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dc4d5-153">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-153">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="dc4d5-154">**To configure Azure AD single sign-on with SAP HANA, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc4d5-154">**To configure Azure AD single sign-on with SAP HANA, take the following steps:**</span></span>

1. <span data-ttu-id="dc4d5-155">In the Azure portal, on the **SAP HANA** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-155">In the Azure portal, on the **SAP HANA** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on][4]

1. <span data-ttu-id="dc4d5-157">In the **Single sign-on** dialog box, under **SAML-based Sign-on**, select **Mode**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-157">In the **Single sign-on** dialog box, under **SAML-based Sign-on**, select **Mode**.</span></span>
 
    ![Single sign-on dialog box](./media/saphana-tutorial/tutorial_saphana_samlbase.png)

1. <span data-ttu-id="dc4d5-159">In the **SAP HANA Domain and URLs** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-159">In the **SAP HANA Domain and URLs** section, take the following steps:</span></span>

    ![Domain and URLs single sign-on information](./media/saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="dc4d5-161">a.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-161">a.</span></span> <span data-ttu-id="dc4d5-162">In the **Identifier** box, type the following: `HA100`</span><span class="sxs-lookup"><span data-stu-id="dc4d5-162">In the **Identifier** box, type the following: `HA100`</span></span> 

    <span data-ttu-id="dc4d5-163">b.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-163">b.</span></span> <span data-ttu-id="dc4d5-164">In the **Reply URL** box, type a URL with the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="dc4d5-164">In the **Reply URL** box, type a URL with the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc4d5-165">These values aren't real.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-165">These values aren't real.</span></span> <span data-ttu-id="dc4d5-166">Update these values with the actual Identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-166">Update these values with the actual Identifier and reply URL.</span></span> <span data-ttu-id="dc4d5-167">Contact the [SAP HANA client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-167">Contact the [SAP HANA client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

1. <span data-ttu-id="dc4d5-168">In the **SAML Signing Certificate** section, select **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-168">In the **SAML Signing Certificate** section, select **Metadata XML**.</span></span> <span data-ttu-id="dc4d5-169">Then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-169">Then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="dc4d5-171">If the certificate isn't active, then make it active by selecting the **Make new certificate active** check box in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-171">If the certificate isn't active, then make it active by selecting the **Make new certificate active** check box in Azure AD.</span></span> 

1. <span data-ttu-id="dc4d5-172">The SAP HANA application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-172">The SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="dc4d5-173">The following screenshot shows an example of this format.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-173">The following screenshot shows an example of this format.</span></span> 

    <span data-ttu-id="dc4d5-174">Here we've mapped the **User Identifier** with the **ExtractMailPrefix()** function of **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-174">Here we've mapped the **User Identifier** with the **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="dc4d5-175">This gives the prefix value of the user's email, which is the unique user ID.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-175">This gives the prefix value of the user's email, which is the unique user ID.</span></span> <span data-ttu-id="dc4d5-176">This user ID is sent to the SAP HANA application in every successful response.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-176">This user ID is sent to the SAP HANA application in every successful response.</span></span>

    ![Configure single sign-on](./media/saphana-tutorial/attribute.png)

1. <span data-ttu-id="dc4d5-178">In the **User Attributes** section of the **Single sign-on** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-178">In the **User Attributes** section of the **Single sign-on** dialog box, take the following steps:</span></span>

    <span data-ttu-id="dc4d5-179">a.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-179">a.</span></span> <span data-ttu-id="dc4d5-180">In the **User Identifier** drop-down list, select **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-180">In the **User Identifier** drop-down list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="dc4d5-181">b.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-181">b.</span></span> <span data-ttu-id="dc4d5-182">In the **Mail** drop-down list, select **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-182">In the **Mail** drop-down list, select **user.mail**.</span></span>

1. <span data-ttu-id="dc4d5-183">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-183">Select the **Save** button.</span></span>

    ![Configure the single sign-on Save button](./media/saphana-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="dc4d5-185">To configure single sign-on on the SAP HANA side, sign in to your **HANA XSA Web Console**  by going to the respective HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-185">To configure single sign-on on the SAP HANA side, sign in to your **HANA XSA Web Console**  by going to the respective HTTPS endpoint.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc4d5-186">In the default configuration, the URL redirects the request to a sign-in screen, which requires the credentials of an authenticated SAP HANA database user.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-186">In the default configuration, the URL redirects the request to a sign-in screen, which requires the credentials of an authenticated SAP HANA database user.</span></span> <span data-ttu-id="dc4d5-187">The user who signs in must have permissions to perform SAML administration tasks.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-187">The user who signs in must have permissions to perform SAML administration tasks.</span></span>

1. <span data-ttu-id="dc4d5-188">In the XSA Web Interface, go to **SAML Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-188">In the XSA Web Interface, go to **SAML Identity Provider**.</span></span> <span data-ttu-id="dc4d5-189">From there, select the **+** button on the bottom of the screen to display the **Add Identity Provider Info** pane.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-189">From there, select the **+** button on the bottom of the screen to display the **Add Identity Provider Info** pane.</span></span> <span data-ttu-id="dc4d5-190">Then take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-190">Then take the following steps:</span></span>

    ![Add Identity Provider](./media/saphana-tutorial/sap1.png)

    <span data-ttu-id="dc4d5-192">a.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-192">a.</span></span> <span data-ttu-id="dc4d5-193">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML (which you downloaded from the Azure portal) into the **Metadata** box.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-193">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML (which you downloaded from the Azure portal) into the **Metadata** box.</span></span>

    ![Add Identity Provider settings](./media/saphana-tutorial/sap2.png)

    <span data-ttu-id="dc4d5-195">b.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-195">b.</span></span> <span data-ttu-id="dc4d5-196">If the contents of the XML document are valid, the parsing process extracts the information that's required for the **Subject, Entity ID, and Issuer** fields in the **General data** screen area.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-196">If the contents of the XML document are valid, the parsing process extracts the information that's required for the **Subject, Entity ID, and Issuer** fields in the **General data** screen area.</span></span> <span data-ttu-id="dc4d5-197">It also extracts the information that's necessary for the URL fields in the **Destination** screen area, for example, the **Base URL and SingleSignOn URL (\*)** fields.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-197">It also extracts the information that's necessary for the URL fields in the **Destination** screen area, for example, the **Base URL and SingleSignOn URL (\*)** fields.</span></span>

    ![Add Identity Provider settings](./media/saphana-tutorial/sap3.png)

    <span data-ttu-id="dc4d5-199">c.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-199">c.</span></span> <span data-ttu-id="dc4d5-200">In the **Name** box of the **General Data** screen area, enter a name for the new SAML SSO identity provider.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-200">In the **Name** box of the **General Data** screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc4d5-201">The name of the SAML IDP is mandatory and must be unique.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-201">The name of the SAML IDP is mandatory and must be unique.</span></span> <span data-ttu-id="dc4d5-202">It appears in the list of available SAML IDPs that is displayed when you select SAML as the authentication method for SAP HANA XS applications to use.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-202">It appears in the list of available SAML IDPs that is displayed when you select SAML as the authentication method for SAP HANA XS applications to use.</span></span> <span data-ttu-id="dc4d5-203">For example, you can do this in the **Authentication** screen area of the XS Artifact Administration tool.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-203">For example, you can do this in the **Authentication** screen area of the XS Artifact Administration tool.</span></span>

1. <span data-ttu-id="dc4d5-204">Select **Save** to save the details of the SAML identity provider and to add the new SAML IDP to the list of known SAML IDPs.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-204">Select **Save** to save the details of the SAML identity provider and to add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![Save button](./media/saphana-tutorial/sap4.png)

1. <span data-ttu-id="dc4d5-206">In HANA Studio, within the system properties of the **Configuration** tab,  filter the settings by **saml**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-206">In HANA Studio, within the system properties of the **Configuration** tab,  filter the settings by **saml**.</span></span> <span data-ttu-id="dc4d5-207">Then adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-207">Then adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![assertion_timeout setting](./media/saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="dc4d5-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dc4d5-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app!</span></span> <span data-ttu-id="dc4d5-210">After you add this app from the **Active Directory** > **Enterprise Applications** section,  select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-210">After you add this app from the **Active Directory** > **Enterprise Applications** section,  select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc4d5-211">You can read more about the embedded documentation feature in the [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dc4d5-211">You can read more about the embedded documentation feature in the [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dc4d5-212">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc4d5-212">Create an Azure AD test user</span></span>
<span data-ttu-id="dc4d5-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD user][100]

<span data-ttu-id="dc4d5-215">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc4d5-215">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="dc4d5-216">In the **Azure portal**, in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-216">In the **Azure portal**, in the left pane, select the **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/saphana-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="dc4d5-218">To display the list of users, go to **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-218">To display the list of users, go to **Users and groups**.</span></span> <span data-ttu-id="dc4d5-219">Then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-219">Then select **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/saphana-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="dc4d5-221">To open the **User** dialog box, select **Add** at the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-221">To open the **User** dialog box, select **Add** at the top of the dialog box.</span></span>
 
    ![The Add button](./media/saphana-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="dc4d5-223">On the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-223">On the **User** dialog box, take the following steps:</span></span>
 
    ![The User dialog box](./media/saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc4d5-225">a.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-225">a.</span></span> <span data-ttu-id="dc4d5-226">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc4d5-227">b.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-227">b.</span></span> <span data-ttu-id="dc4d5-228">In the **User name** box, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-228">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc4d5-229">c.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-229">c.</span></span> <span data-ttu-id="dc4d5-230">Select **Show Password**, and then write down the password.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-230">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="dc4d5-231">d.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-231">d.</span></span> <span data-ttu-id="dc4d5-232">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-232">Select **Create**.</span></span>
 
### <a name="create-a-sap-hana-test-user"></a><span data-ttu-id="dc4d5-233">Create a SAP HANA test user</span><span class="sxs-lookup"><span data-stu-id="dc4d5-233">Create a SAP HANA test user</span></span>

<span data-ttu-id="dc4d5-234">To enable Azure AD users to sign in to SAP HANA, you must provision them in SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-234">To enable Azure AD users to sign in to SAP HANA, you must provision them in SAP HANA.</span></span>
<span data-ttu-id="dc4d5-235">SAP HANA supports just-in-time provisioning, which is by enabled by default.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-235">SAP HANA supports just-in-time provisioning, which is by enabled by default.</span></span>

<span data-ttu-id="dc4d5-236">If you need to create a user manually, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc4d5-236">If you need to create a user manually, take the following steps:</span></span>

>[!NOTE]
><span data-ttu-id="dc4d5-237">You can change the external authentication that the user uses.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-237">You can change the external authentication that the user uses.</span></span> <span data-ttu-id="dc4d5-238">They can authenticate with an external system such as Kerberos.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-238">They can authenticate with an external system such as Kerberos.</span></span> <span data-ttu-id="dc4d5-239">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="dc4d5-239">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="dc4d5-240">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator, and then enable the DB-User for SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-240">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator, and then enable the DB-User for SAML SSO.</span></span>

    ![Create user](./media/saphana-tutorial/sap5.png)

1. <span data-ttu-id="dc4d5-242">Select the invisible check box to the left of **SAML**, and then select the **Configure** link.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-242">Select the invisible check box to the left of **SAML**, and then select the **Configure** link.</span></span>

1. <span data-ttu-id="dc4d5-243">Select **Add** to add the SAML IDP.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-243">Select **Add** to add the SAML IDP.</span></span>  <span data-ttu-id="dc4d5-244">Select the appropriate SAML IDP, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-244">Select the appropriate SAML IDP, and then select **OK**.</span></span>

1. <span data-ttu-id="dc4d5-245">Add the **External Identity** (in this case, BrittaSimon) or choose **Any**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-245">Add the **External Identity** (in this case, BrittaSimon) or choose **Any**.</span></span> <span data-ttu-id="dc4d5-246">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-246">Then select **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="dc4d5-247">If  the **Any** check box is not selected, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-247">If  the **Any** check box is not selected, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix.</span></span> <span data-ttu-id="dc4d5-248">(For example, BrittaSimon@contoso.com becomes BrittaSimon in HANA.)</span><span class="sxs-lookup"><span data-stu-id="dc4d5-248">(For example, BrittaSimon@contoso.com becomes BrittaSimon in HANA.)</span></span>

1. <span data-ttu-id="dc4d5-249">For testing purposes, assign all **XS** roles to the user.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-249">For testing purposes, assign all **XS** roles to the user.</span></span>

    ![Assigning roles](./media/saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="dc4d5-251">You should give permissions that are appropriate for your use cases only.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-251">You should give permissions that are appropriate for your use cases only.</span></span>

1. <span data-ttu-id="dc4d5-252">Save the user.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-252">Save the user.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dc4d5-253">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc4d5-253">Assign the Azure AD test user</span></span>

<span data-ttu-id="dc4d5-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Assign the user role][200] 

<span data-ttu-id="dc4d5-256">**To assign Britta Simon to SAP HANA, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc4d5-256">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="dc4d5-257">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-257">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="dc4d5-258">Go to the directory view, and go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-258">Go to the directory view, and go to **Enterprise applications**.</span></span> <span data-ttu-id="dc4d5-259">Select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-259">Select **All applications**.</span></span>

    ![Assign user][201] 

1. <span data-ttu-id="dc4d5-261">In the applications list, select **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-261">In the applications list, select **SAP HANA**.</span></span>

    ![Assign user](./media/saphana-tutorial/tutorial_saphana_app.png) 

1. <span data-ttu-id="dc4d5-263">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-263">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="dc4d5-265">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-265">Select the **Add** button.</span></span> <span data-ttu-id="dc4d5-266">In the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-266">In the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="dc4d5-268">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-268">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span></span>

1. <span data-ttu-id="dc4d5-269">Click the **Select** button in the **Users and groups** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-269">Click the **Select** button in the **Users and groups** dialog box.</span></span>

1. <span data-ttu-id="dc4d5-270">Select the **Assign** button in the **Add Assignment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-270">Select the **Assign** button in the **Add Assignment** dialog box.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dc4d5-271">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc4d5-271">Test single sign-on</span></span>

<span data-ttu-id="dc4d5-272">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-272">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="dc4d5-273">When you select the SAP HANA tile in the access panel, you should get automatically signed into your SAP HANA application.</span><span class="sxs-lookup"><span data-stu-id="dc4d5-273">When you select the SAP HANA tile in the access panel, you should get automatically signed into your SAP HANA application.</span></span>
<span data-ttu-id="dc4d5-274">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc4d5-274">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc4d5-275">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dc4d5-275">Additional resources</span></span>

* [<span data-ttu-id="dc4d5-276">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc4d5-276">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dc4d5-277">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc4d5-277">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/saphana-tutorial/tutorial_general_01.png
[2]: ./media/saphana-tutorial/tutorial_general_02.png
[3]: ./media/saphana-tutorial/tutorial_general_03.png
[4]: ./media/saphana-tutorial/tutorial_general_04.png

[100]: ./media/saphana-tutorial/tutorial_general_100.png

[200]: ./media/saphana-tutorial/tutorial_general_200.png
[201]: ./media/saphana-tutorial/tutorial_general_201.png
[202]: ./media/saphana-tutorial/tutorial_general_202.png
[203]: ./media/saphana-tutorial/tutorial_general_203.png

