---
title: 'Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP HANA Cloud Platform Identity Authentication.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 68b1d30f1597946594320a03feed09e494786981
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550167"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="02df8-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="02df8-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="02df8-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02df8-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="02df8-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span><span class="sxs-lookup"><span data-stu-id="02df8-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="02df8-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="02df8-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02df8-107">You can control in Azure AD who has access to SAP application</span><span class="sxs-lookup"><span data-stu-id="02df8-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="02df8-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="02df8-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="02df8-109">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="02df8-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="02df8-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02df8-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="02df8-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02df8-111">Prerequisites</span></span>

<span data-ttu-id="02df8-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="02df8-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="02df8-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="02df8-113">An Azure AD subscription</span></span>
- <span data-ttu-id="02df8-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="02df8-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="02df8-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="02df8-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="02df8-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="02df8-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02df8-117">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="02df8-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="02df8-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02df8-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02df8-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="02df8-119">Scenario description</span></span>
<span data-ttu-id="02df8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="02df8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="02df8-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="02df8-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02df8-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span><span class="sxs-lookup"><span data-stu-id="02df8-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="02df8-123">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="02df8-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="02df8-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span><span class="sxs-lookup"><span data-stu-id="02df8-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="02df8-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="02df8-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span><span class="sxs-lookup"><span data-stu-id="02df8-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="02df8-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span><span class="sxs-lookup"><span data-stu-id="02df8-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="02df8-128">The following diagram illustrates this:</span><span class="sxs-lookup"><span data-stu-id="02df8-128">The following diagram illustrates this:</span></span>    

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/architecture-01.png)

<span data-ttu-id="02df8-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="02df8-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="02df8-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span><span class="sxs-lookup"><span data-stu-id="02df8-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="02df8-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="02df8-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="02df8-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span><span class="sxs-lookup"><span data-stu-id="02df8-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="02df8-134">Currently Web SSO has been tested by both parties, only.</span><span class="sxs-lookup"><span data-stu-id="02df8-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="02df8-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span><span class="sxs-lookup"><span data-stu-id="02df8-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="02df8-136">They will be tested as part of subsequent activities.</span><span class="sxs-lookup"><span data-stu-id="02df8-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="02df8-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span><span class="sxs-lookup"><span data-stu-id="02df8-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="02df8-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="02df8-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02df8-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02df8-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02df8-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="02df8-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02df8-142">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="02df8-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02df8-143">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="02df8-143">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="02df8-145">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-145">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="02df8-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="02df8-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="02df8-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="02df8-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="02df8-151">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02df8-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="02df8-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02df8-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02df8-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02df8-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="02df8-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span><span class="sxs-lookup"><span data-stu-id="02df8-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="02df8-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="02df8-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="02df8-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02df8-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="02df8-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02df8-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02df8-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02df8-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="02df8-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="02df8-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02df8-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02df8-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="02df8-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="02df8-162">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="02df8-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="02df8-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span><span class="sxs-lookup"><span data-stu-id="02df8-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="02df8-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="02df8-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="02df8-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="02df8-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="02df8-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="02df8-166">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="02df8-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02df8-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="02df8-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="02df8-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="02df8-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="02df8-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On][5]

3. <span data-ttu-id="02df8-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span><span class="sxs-lookup"><span data-stu-id="02df8-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="02df8-174">On the SAML token attributes dialog, add the "firstName" attribute.</span><span class="sxs-lookup"><span data-stu-id="02df8-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="02df8-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Configure Single Sign-On][6]

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="02df8-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span><span class="sxs-lookup"><span data-stu-id="02df8-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="02df8-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="02df8-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="02df8-180">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="02df8-180">Click **Ok**.</span></span>

4. <span data-ttu-id="02df8-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02df8-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="02df8-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span><span class="sxs-lookup"><span data-stu-id="02df8-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="02df8-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="02df8-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="02df8-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="02df8-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="02df8-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="02df8-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="02df8-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="02df8-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span><span class="sxs-lookup"><span data-stu-id="02df8-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="02df8-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="02df8-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="02df8-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="02df8-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="02df8-193">In the Azure Management portal, click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="02df8-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="02df8-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span><span class="sxs-lookup"><span data-stu-id="02df8-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="02df8-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="02df8-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="02df8-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configure Linked Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/linked_sign_on.png)
10. <span data-ttu-id="02df8-198">Then, save the configuration.</span><span class="sxs-lookup"><span data-stu-id="02df8-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="02df8-199">The new application will leverage the SSO configuration for the previous SAP application.</span><span class="sxs-lookup"><span data-stu-id="02df8-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="02df8-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span><span class="sxs-lookup"><span data-stu-id="02df8-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="02df8-201">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02df8-201">Create an Azure AD test user</span></span>
<span data-ttu-id="02df8-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02df8-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="02df8-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02df8-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02df8-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="02df8-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02df8-207">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="02df8-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02df8-209">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02df8-211">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02df8-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="02df8-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02df8-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="02df8-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02df8-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="02df8-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="02df8-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="02df8-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="02df8-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="02df8-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span><span class="sxs-lookup"><span data-stu-id="02df8-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="02df8-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="02df8-219">Users who are in the Azure AD user store can use the SSO functionality.</span><span class="sxs-lookup"><span data-stu-id="02df8-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="02df8-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span><span class="sxs-lookup"><span data-stu-id="02df8-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="02df8-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="02df8-222">In the default setting, the Identity Federation option is disabled.</span><span class="sxs-lookup"><span data-stu-id="02df8-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="02df8-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span><span class="sxs-lookup"><span data-stu-id="02df8-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="02df8-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="02df8-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="02df8-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02df8-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="02df8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="02df8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Assign User][200] 

<span data-ttu-id="02df8-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02df8-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="02df8-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="02df8-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="02df8-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="02df8-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="02df8-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="02df8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="02df8-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="02df8-235">Click **Add** button.</span></span> <span data-ttu-id="02df8-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="02df8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="02df8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02df8-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02df8-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="02df8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="02df8-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="02df8-241">Test single sign-on</span></span>

<span data-ttu-id="02df8-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="02df8-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="02df8-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span><span class="sxs-lookup"><span data-stu-id="02df8-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="02df8-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="02df8-244">Additional resources</span></span>

* [<span data-ttu-id="02df8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02df8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02df8-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02df8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_06.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-tutorial/tutorial_general_203.png
























