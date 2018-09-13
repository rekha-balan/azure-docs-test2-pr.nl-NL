---
title: 'Tutorial: Azure Active Directory integration with SAP Business ByDesign | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a7a08eb6062f134058bb63f5a3e2a78f661026ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864778"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="d803c-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="d803c-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="d803c-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d803c-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d803c-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d803c-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d803c-106">You can control in Azure AD who has access to SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="d803c-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="d803c-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d803c-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d803c-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d803c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d803c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d803c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d803c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d803c-110">Prerequisites</span></span>

<span data-ttu-id="d803c-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d803c-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="d803c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d803c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d803c-113">An SAP Business ByDesign single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d803c-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d803c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d803c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d803c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d803c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d803c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d803c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d803c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d803c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d803c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d803c-118">Scenario description</span></span>
<span data-ttu-id="d803c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d803c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d803c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d803c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d803c-121">Adding SAP Business ByDesign from the gallery</span><span class="sxs-lookup"><span data-stu-id="d803c-121">Adding SAP Business ByDesign from the gallery</span></span>
1. <span data-ttu-id="d803c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d803c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="d803c-123">Adding SAP Business ByDesign from the gallery</span><span class="sxs-lookup"><span data-stu-id="d803c-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="d803c-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d803c-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d803c-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d803c-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d803c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d803c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d803c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d803c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d803c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d803c-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d803c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d803c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d803c-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d803c-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign in the results list](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d803c-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d803c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d803c-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d803c-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d803c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d803c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="d803c-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d803c-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="d803c-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d803c-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d803c-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d803c-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d803c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d803c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d803c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d803c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d803c-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d803c-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d803c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d803c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d803c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d803c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d803c-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d803c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d803c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span><span class="sxs-lookup"><span data-stu-id="d803c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="d803c-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d803c-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="d803c-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d803c-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d803c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d803c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

1. <span data-ttu-id="d803c-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d803c-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![SAP Business ByDesign Domain and URLs single sign-on information](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="d803c-155">a.</span><span class="sxs-lookup"><span data-stu-id="d803c-155">a.</span></span> <span data-ttu-id="d803c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="d803c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="d803c-157">b.</span><span class="sxs-lookup"><span data-stu-id="d803c-157">b.</span></span> <span data-ttu-id="d803c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="d803c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d803c-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d803c-159">These values are not real.</span></span> <span data-ttu-id="d803c-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="d803c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d803c-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d803c-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

1. <span data-ttu-id="d803c-162">On the **User Attributes** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d803c-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![SAP Business ByDesign Attribute Section](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="d803c-164">a.</span><span class="sxs-lookup"><span data-stu-id="d803c-164">a.</span></span> <span data-ttu-id="d803c-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span><span class="sxs-lookup"><span data-stu-id="d803c-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="d803c-166">b.</span><span class="sxs-lookup"><span data-stu-id="d803c-166">b.</span></span> <span data-ttu-id="d803c-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="d803c-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="d803c-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="d803c-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

1. <span data-ttu-id="d803c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d803c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

1. <span data-ttu-id="d803c-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d803c-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sapbusinessbydesign-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d803c-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d803c-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d803c-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d803c-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign Configuration](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

1. <span data-ttu-id="d803c-176">To get SSO configured for your application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d803c-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="d803c-177">a.</span><span class="sxs-lookup"><span data-stu-id="d803c-177">a.</span></span> <span data-ttu-id="d803c-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span><span class="sxs-lookup"><span data-stu-id="d803c-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="d803c-179">b.</span><span class="sxs-lookup"><span data-stu-id="d803c-179">b.</span></span> <span data-ttu-id="d803c-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="d803c-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="d803c-181">c.</span><span class="sxs-lookup"><span data-stu-id="d803c-181">c.</span></span> <span data-ttu-id="d803c-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d803c-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="d803c-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span><span class="sxs-lookup"><span data-stu-id="d803c-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configure Single Sign-On](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="d803c-185">d.</span><span class="sxs-lookup"><span data-stu-id="d803c-185">d.</span></span> <span data-ttu-id="d803c-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span><span class="sxs-lookup"><span data-stu-id="d803c-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="d803c-187">e.</span><span class="sxs-lookup"><span data-stu-id="d803c-187">e.</span></span> <span data-ttu-id="d803c-188">Click **Activate Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d803c-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="d803c-189">f.</span><span class="sxs-lookup"><span data-stu-id="d803c-189">f.</span></span> <span data-ttu-id="d803c-190">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="d803c-190">Save your changes.</span></span>
   
    <span data-ttu-id="d803c-191">g.</span><span class="sxs-lookup"><span data-stu-id="d803c-191">g.</span></span> <span data-ttu-id="d803c-192">Click the **My System** tab.</span><span class="sxs-lookup"><span data-stu-id="d803c-192">Click the **My System** tab.</span></span>
   
    ![Configure Single Sign-On](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="d803c-194">h.</span><span class="sxs-lookup"><span data-stu-id="d803c-194">h.</span></span> <span data-ttu-id="d803c-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d803c-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configure Single Sign-On](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="d803c-197">i.</span><span class="sxs-lookup"><span data-stu-id="d803c-197">i.</span></span> <span data-ttu-id="d803c-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span><span class="sxs-lookup"><span data-stu-id="d803c-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="d803c-199">j.</span><span class="sxs-lookup"><span data-stu-id="d803c-199">j.</span></span> <span data-ttu-id="d803c-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span><span class="sxs-lookup"><span data-stu-id="d803c-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="d803c-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span><span class="sxs-lookup"><span data-stu-id="d803c-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="d803c-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="d803c-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="d803c-203">The system sends only the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="d803c-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="d803c-204">The employee cannot log on using SSO, and must use password or certificate instead.</span><span class="sxs-lookup"><span data-stu-id="d803c-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="d803c-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="d803c-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="d803c-206">The system sends only the SSO URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="d803c-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="d803c-207">The employee can log on using SSO.</span><span class="sxs-lookup"><span data-stu-id="d803c-207">The employee can log on using SSO.</span></span> <span data-ttu-id="d803c-208">Authentication request is redirected through the IdP.</span><span class="sxs-lookup"><span data-stu-id="d803c-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="d803c-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="d803c-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="d803c-210">If SSO is not active, the system sends the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="d803c-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="d803c-211">If SSO is active, the system checks whether the employee has a password.</span><span class="sxs-lookup"><span data-stu-id="d803c-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="d803c-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="d803c-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="d803c-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="d803c-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="d803c-214">k.</span><span class="sxs-lookup"><span data-stu-id="d803c-214">k.</span></span> <span data-ttu-id="d803c-215">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="d803c-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="d803c-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d803c-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d803c-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d803c-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d803c-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d803c-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d803c-219">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d803c-219">Create an Azure AD test user</span></span>

<span data-ttu-id="d803c-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d803c-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d803c-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d803c-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d803c-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d803c-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sapbusinessbydesign-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d803c-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d803c-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sapbusinessbydesign-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d803c-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d803c-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sapbusinessbydesign-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d803c-229">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d803c-229">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d803c-231">a.</span><span class="sxs-lookup"><span data-stu-id="d803c-231">a.</span></span> <span data-ttu-id="d803c-232">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d803c-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d803c-233">b.</span><span class="sxs-lookup"><span data-stu-id="d803c-233">b.</span></span> <span data-ttu-id="d803c-234">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d803c-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d803c-235">c.</span><span class="sxs-lookup"><span data-stu-id="d803c-235">c.</span></span> <span data-ttu-id="d803c-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d803c-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d803c-237">d.</span><span class="sxs-lookup"><span data-stu-id="d803c-237">d.</span></span> <span data-ttu-id="d803c-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d803c-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="d803c-239">Create an SAP Business ByDesign test user</span><span class="sxs-lookup"><span data-stu-id="d803c-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="d803c-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="d803c-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="d803c-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span><span class="sxs-lookup"><span data-stu-id="d803c-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="d803c-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span><span class="sxs-lookup"><span data-stu-id="d803c-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d803c-243">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d803c-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="d803c-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="d803c-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d803c-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d803c-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="d803c-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d803c-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d803c-249">In the applications list, select **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="d803c-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![The SAP Business ByDesign link in the Applications list](./media/sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

1. <span data-ttu-id="d803c-251">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d803c-251">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d803c-253">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d803c-253">Click **Add** button.</span></span> <span data-ttu-id="d803c-254">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d803c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d803c-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d803c-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d803c-257">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d803c-257">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d803c-258">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d803c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d803c-259">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d803c-259">Test single sign-on</span></span>

<span data-ttu-id="d803c-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d803c-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d803c-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span><span class="sxs-lookup"><span data-stu-id="d803c-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d803c-262">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d803c-262">Additional resources</span></span>

* [<span data-ttu-id="d803c-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d803c-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d803c-264">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d803c-264">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/sapbusinessbydesign-tutorial/tutorial_general_203.png

