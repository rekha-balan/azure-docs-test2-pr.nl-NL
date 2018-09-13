---
title: 'Tutorial: Azure Active Directory integration with SAP Cloud for Customer | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Cloud for Customer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 59bbcbf9aaef17394151e7db1471b63b87a46288
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864454"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="4a9da-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="4a9da-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="4a9da-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a9da-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a9da-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4a9da-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4a9da-106">You can control in Azure AD who has access to SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="4a9da-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="4a9da-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4a9da-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a9da-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a9da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4a9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4a9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a9da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4a9da-110">Prerequisites</span></span>

<span data-ttu-id="4a9da-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4a9da-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="4a9da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4a9da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a9da-113">A SAP Cloud for Customer single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4a9da-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4a9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a9da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4a9da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a9da-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4a9da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a9da-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a9da-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a9da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4a9da-118">Scenario description</span></span>
<span data-ttu-id="4a9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4a9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4a9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a9da-121">Adding SAP Cloud for Customer from the gallery</span><span class="sxs-lookup"><span data-stu-id="4a9da-121">Adding SAP Cloud for Customer from the gallery</span></span>
1. <span data-ttu-id="4a9da-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a9da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="4a9da-123">Adding SAP Cloud for Customer from the gallery</span><span class="sxs-lookup"><span data-stu-id="4a9da-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="4a9da-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4a9da-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4a9da-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a9da-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4a9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4a9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4a9da-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4a9da-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4a9da-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4a9da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4a9da-133">In the search box, type **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

1. <span data-ttu-id="4a9da-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4a9da-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a9da-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a9da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a9da-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a9da-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a9da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a9da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="4a9da-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4a9da-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="4a9da-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4a9da-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4a9da-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4a9da-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4a9da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4a9da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4a9da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a9da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4a9da-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4a9da-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4a9da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a9da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4a9da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4a9da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a9da-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a9da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a9da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span><span class="sxs-lookup"><span data-stu-id="4a9da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="4a9da-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a9da-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="4a9da-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4a9da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a9da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

1. <span data-ttu-id="4a9da-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a9da-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="4a9da-157">a.</span><span class="sxs-lookup"><span data-stu-id="4a9da-157">a.</span></span> <span data-ttu-id="4a9da-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="4a9da-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="4a9da-159">b.</span><span class="sxs-lookup"><span data-stu-id="4a9da-159">b.</span></span> <span data-ttu-id="4a9da-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="4a9da-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a9da-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4a9da-161">These values are not real.</span></span> <span data-ttu-id="4a9da-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="4a9da-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4a9da-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4a9da-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

1. <span data-ttu-id="4a9da-164">On the **User Attributes** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a9da-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="4a9da-166">a.</span><span class="sxs-lookup"><span data-stu-id="4a9da-166">a.</span></span> <span data-ttu-id="4a9da-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span><span class="sxs-lookup"><span data-stu-id="4a9da-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="4a9da-168">b.</span><span class="sxs-lookup"><span data-stu-id="4a9da-168">b.</span></span> <span data-ttu-id="4a9da-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="4a9da-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="4a9da-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="4a9da-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

1. <span data-ttu-id="4a9da-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4a9da-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

1. <span data-ttu-id="4a9da-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4a9da-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4a9da-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4a9da-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4a9da-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4a9da-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

1. <span data-ttu-id="4a9da-178">To get SSO configured, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a9da-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="4a9da-179">a.</span><span class="sxs-lookup"><span data-stu-id="4a9da-179">a.</span></span> <span data-ttu-id="4a9da-180">Login into SAP Cloud for Customer portal with administrator rights.</span><span class="sxs-lookup"><span data-stu-id="4a9da-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="4a9da-181">b.</span><span class="sxs-lookup"><span data-stu-id="4a9da-181">b.</span></span> <span data-ttu-id="4a9da-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="4a9da-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="4a9da-183">c.</span><span class="sxs-lookup"><span data-stu-id="4a9da-183">c.</span></span> <span data-ttu-id="4a9da-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4a9da-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="4a9da-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span><span class="sxs-lookup"><span data-stu-id="4a9da-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="4a9da-187">d.</span><span class="sxs-lookup"><span data-stu-id="4a9da-187">d.</span></span> <span data-ttu-id="4a9da-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span><span class="sxs-lookup"><span data-stu-id="4a9da-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="4a9da-189">e.</span><span class="sxs-lookup"><span data-stu-id="4a9da-189">e.</span></span> <span data-ttu-id="4a9da-190">Click **Activate Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="4a9da-191">f.</span><span class="sxs-lookup"><span data-stu-id="4a9da-191">f.</span></span> <span data-ttu-id="4a9da-192">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4a9da-192">Save your changes.</span></span>
   
    <span data-ttu-id="4a9da-193">g.</span><span class="sxs-lookup"><span data-stu-id="4a9da-193">g.</span></span> <span data-ttu-id="4a9da-194">Click the **My System** tab.</span><span class="sxs-lookup"><span data-stu-id="4a9da-194">Click the **My System** tab.</span></span>
   
    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="4a9da-196">h.</span><span class="sxs-lookup"><span data-stu-id="4a9da-196">h.</span></span> <span data-ttu-id="4a9da-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4a9da-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="4a9da-199">i.</span><span class="sxs-lookup"><span data-stu-id="4a9da-199">i.</span></span> <span data-ttu-id="4a9da-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="4a9da-201">j.</span><span class="sxs-lookup"><span data-stu-id="4a9da-201">j.</span></span> <span data-ttu-id="4a9da-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span><span class="sxs-lookup"><span data-stu-id="4a9da-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="4a9da-203">In the **URL Sent to Employee** list, you can choose between the following options:</span><span class="sxs-lookup"><span data-stu-id="4a9da-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="4a9da-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="4a9da-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="4a9da-205">The system sends only the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="4a9da-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="4a9da-206">The employee cannot log on using SSO, and must use password or certificate instead.</span><span class="sxs-lookup"><span data-stu-id="4a9da-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="4a9da-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="4a9da-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="4a9da-208">The system sends only the SSO URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="4a9da-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="4a9da-209">The employee can log on using SSO.</span><span class="sxs-lookup"><span data-stu-id="4a9da-209">The employee can log on using SSO.</span></span> <span data-ttu-id="4a9da-210">Authentication request is redirected through the IdP.</span><span class="sxs-lookup"><span data-stu-id="4a9da-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="4a9da-211">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="4a9da-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="4a9da-212">If SSO is not active, the system sends the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="4a9da-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="4a9da-213">If SSO is active, the system checks whether the employee has a password.</span><span class="sxs-lookup"><span data-stu-id="4a9da-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="4a9da-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="4a9da-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="4a9da-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="4a9da-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="4a9da-216">k.</span><span class="sxs-lookup"><span data-stu-id="4a9da-216">k.</span></span> <span data-ttu-id="4a9da-217">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="4a9da-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="4a9da-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4a9da-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4a9da-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4a9da-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4a9da-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a9da-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a9da-221">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4a9da-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a9da-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a9da-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4a9da-224">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a9da-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4a9da-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4a9da-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4a9da-227">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4a9da-229">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4a9da-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4a9da-231">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a9da-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a9da-233">a.</span><span class="sxs-lookup"><span data-stu-id="4a9da-233">a.</span></span> <span data-ttu-id="4a9da-234">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a9da-235">b.</span><span class="sxs-lookup"><span data-stu-id="4a9da-235">b.</span></span> <span data-ttu-id="4a9da-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a9da-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a9da-237">c.</span><span class="sxs-lookup"><span data-stu-id="4a9da-237">c.</span></span> <span data-ttu-id="4a9da-238">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4a9da-239">d.</span><span class="sxs-lookup"><span data-stu-id="4a9da-239">d.</span></span> <span data-ttu-id="4a9da-240">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="4a9da-241">Creating a SAP Cloud for Customer test user</span><span class="sxs-lookup"><span data-stu-id="4a9da-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="4a9da-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="4a9da-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="4a9da-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span><span class="sxs-lookup"><span data-stu-id="4a9da-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a9da-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span><span class="sxs-lookup"><span data-stu-id="4a9da-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4a9da-245">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4a9da-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4a9da-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="4a9da-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Assign User][200] 

<span data-ttu-id="4a9da-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a9da-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="4a9da-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4a9da-251">In the applications list, select **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configure Single Sign-On](./media/sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

1. <span data-ttu-id="4a9da-253">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4a9da-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4a9da-255">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4a9da-255">Click **Add** button.</span></span> <span data-ttu-id="4a9da-256">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a9da-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4a9da-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4a9da-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4a9da-259">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a9da-259">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4a9da-260">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a9da-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a9da-261">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a9da-261">Testing single sign-on</span></span>

<span data-ttu-id="4a9da-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4a9da-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4a9da-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span><span class="sxs-lookup"><span data-stu-id="4a9da-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="4a9da-264">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a9da-264">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a9da-265">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4a9da-265">Additional resources</span></span>

* [<span data-ttu-id="4a9da-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a9da-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4a9da-267">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a9da-267">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/sap-customer-cloud-tutorial/tutorial_general_203.png

