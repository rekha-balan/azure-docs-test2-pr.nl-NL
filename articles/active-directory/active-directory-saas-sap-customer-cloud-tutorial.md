---
title: 'Tutorial: Azure Active Directory integration with SAP Cloud for Customer | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Cloud for Customer.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 4bf18956181b371f6cb767e8106e536f2a452725
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670031"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="02e26-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="02e26-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>
<span data-ttu-id="02e26-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02e26-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02e26-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="02e26-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="02e26-106">You can control in Azure AD who has access to SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="02e26-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
* <span data-ttu-id="02e26-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="02e26-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="02e26-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="02e26-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="02e26-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02e26-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02e26-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02e26-110">Prerequisites</span></span>
<span data-ttu-id="02e26-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="02e26-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

* <span data-ttu-id="02e26-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="02e26-112">An Azure AD subscription</span></span>
* <span data-ttu-id="02e26-113">A SAP Cloud for Customer single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="02e26-113">A SAP Cloud for Customer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02e26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="02e26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="02e26-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="02e26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="02e26-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="02e26-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="02e26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02e26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02e26-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="02e26-118">Scenario description</span></span>
<span data-ttu-id="02e26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="02e26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="02e26-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="02e26-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02e26-121">Adding SAP Cloud for Customer from the gallery</span><span class="sxs-lookup"><span data-stu-id="02e26-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="02e26-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02e26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="02e26-123">Adding SAP Cloud for Customer from the gallery</span><span class="sxs-lookup"><span data-stu-id="02e26-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="02e26-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="02e26-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02e26-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02e26-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02e26-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02e26-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="02e26-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="02e26-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="02e26-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="02e26-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="02e26-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="02e26-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="02e26-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="02e26-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="02e26-135">In the search box, type **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="02e26-135">In the search box, type **SAP Cloud for Customer**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_01.png)

7. <span data-ttu-id="02e26-137">In the results pane, select **SAP Cloud for Customer**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="02e26-137">In the results pane, select **SAP Cloud for Customer**, and then click **Complete** to add the application.</span></span>
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02e26-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02e26-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02e26-140">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02e26-140">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02e26-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02e26-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="02e26-142">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span><span class="sxs-lookup"><span data-stu-id="02e26-142">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="02e26-143">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="02e26-143">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02e26-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="02e26-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02e26-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02e26-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02e26-146">**[Creating a SAP Cloud for Customer test user](#creating-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="02e26-146">**[Creating a SAP Cloud for Customer test user](#creating-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="02e26-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02e26-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02e26-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="02e26-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02e26-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02e26-149">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="02e26-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP Cloud for Customer application.</span><span class="sxs-lookup"><span data-stu-id="02e26-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP Cloud for Customer application.</span></span> 

<span data-ttu-id="02e26-151">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02e26-151">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="02e26-152">In the Azure classic portal, on the **SAP Cloud for Customer** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="02e26-152">In the Azure classic portal, on the **SAP Cloud for Customer** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_80.png) 

2. <span data-ttu-id="02e26-154">In the attributes SAML token attributes list, select the nameidentifier attribute, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="02e26-154">In the attributes SAML token attributes list, select the nameidentifier attribute, and then click **Edit**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_84.png) 

3. <span data-ttu-id="02e26-156">On the **Edit User Attribute** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-156">On the **Edit User Attribute** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_85.png) 

    <span data-ttu-id="02e26-158">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-158">a.</span></span> <span data-ttu-id="02e26-159">From the **Attribute Value** list, select the **ExtractMailPrefix()** fuction.</span><span class="sxs-lookup"><span data-stu-id="02e26-159">From the **Attribute Value** list, select the **ExtractMailPrefix()** fuction.</span></span>

    <span data-ttu-id="02e26-160">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-160">b.</span></span> <span data-ttu-id="02e26-161">From the **Mail** list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="02e26-161">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> 
    <span data-ttu-id="02e26-162">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="02e26-162">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span> 

    <span data-ttu-id="02e26-163">c.</span><span class="sxs-lookup"><span data-stu-id="02e26-163">c.</span></span> <span data-ttu-id="02e26-164">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="02e26-164">Click **Complete**.</span></span> 


1. <span data-ttu-id="02e26-165">In the classic portal, on the **SAP Cloud for Customer** application integration page, click **Configure single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="02e26-165">In the classic portal, on the **SAP Cloud for Customer** application integration page, click **Configure single sign-on**.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="02e26-167">On the **How would you like users to sign on to SAP Cloud for Customer** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02e26-167">On the **How would you like users to sign on to SAP Cloud for Customer** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_03.png) 

3. <span data-ttu-id="02e26-169">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-169">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_04.png) 
   
    <span data-ttu-id="02e26-171">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-171">a.</span></span> <span data-ttu-id="02e26-172">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP Cloud for Customer application using the following pattern: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="02e26-172">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP Cloud for Customer application using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>
   
    <span data-ttu-id="02e26-173">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-173">b.</span></span> <span data-ttu-id="02e26-174">click **Next**</span><span class="sxs-lookup"><span data-stu-id="02e26-174">click **Next**</span></span>

4. <span data-ttu-id="02e26-175">On the **Configure single sign-on at SAP Cloud for Customer** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-175">On the **Configure single sign-on at SAP Cloud for Customer** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_05.png)
   
    <span data-ttu-id="02e26-177">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-177">a.</span></span> <span data-ttu-id="02e26-178">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="02e26-178">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="02e26-179">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-179">b.</span></span> <span data-ttu-id="02e26-180">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02e26-180">Click **Next**.</span></span>

5. <span data-ttu-id="02e26-181">To get SSO configured, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-181">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="02e26-182">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-182">a.</span></span> <span data-ttu-id="02e26-183">Login into SAP Cloud for Customer portal with administrator rights.</span><span class="sxs-lookup"><span data-stu-id="02e26-183">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="02e26-184">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-184">b.</span></span> <span data-ttu-id="02e26-185">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="02e26-185">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="02e26-186">c.</span><span class="sxs-lookup"><span data-stu-id="02e26-186">c.</span></span> <span data-ttu-id="02e26-187">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="02e26-187">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure classic portal.</span></span> <span data-ttu-id="02e26-188">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span><span class="sxs-lookup"><span data-stu-id="02e26-188">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="02e26-190">d.</span><span class="sxs-lookup"><span data-stu-id="02e26-190">d.</span></span> <span data-ttu-id="02e26-191">Azure AD requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span><span class="sxs-lookup"><span data-stu-id="02e26-191">Azure AD requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="02e26-192">e.</span><span class="sxs-lookup"><span data-stu-id="02e26-192">e.</span></span> <span data-ttu-id="02e26-193">Click **Activate Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="02e26-193">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="02e26-194">f.</span><span class="sxs-lookup"><span data-stu-id="02e26-194">f.</span></span> <span data-ttu-id="02e26-195">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="02e26-195">Save your changes.</span></span>
   
    <span data-ttu-id="02e26-196">g.</span><span class="sxs-lookup"><span data-stu-id="02e26-196">g.</span></span> <span data-ttu-id="02e26-197">Click the **My System** tab.</span><span class="sxs-lookup"><span data-stu-id="02e26-197">Click the **My System** tab.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="02e26-199">h.</span><span class="sxs-lookup"><span data-stu-id="02e26-199">h.</span></span> <span data-ttu-id="02e26-200">Copy the **SSO URL** and paste it into the **Azure AD Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="02e26-200">Copy the **SSO URL** and paste it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="02e26-202">i.</span><span class="sxs-lookup"><span data-stu-id="02e26-202">i.</span></span> <span data-ttu-id="02e26-203">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span><span class="sxs-lookup"><span data-stu-id="02e26-203">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="02e26-204">j.</span><span class="sxs-lookup"><span data-stu-id="02e26-204">j.</span></span> <span data-ttu-id="02e26-205">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span><span class="sxs-lookup"><span data-stu-id="02e26-205">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="02e26-206">In the **URL Sent to Employee** list, you can choose between the following options:</span><span class="sxs-lookup"><span data-stu-id="02e26-206">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="02e26-207">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="02e26-207">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="02e26-208">The system sends only the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="02e26-208">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="02e26-209">The employee cannot log on using SSO, and must use password or certificate instead.</span><span class="sxs-lookup"><span data-stu-id="02e26-209">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="02e26-210">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="02e26-210">**SSO URL**</span></span> 
   
    <span data-ttu-id="02e26-211">The system sends only the SSO URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="02e26-211">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="02e26-212">The employee can log on using SSO.</span><span class="sxs-lookup"><span data-stu-id="02e26-212">The employee can log on using SSO.</span></span> <span data-ttu-id="02e26-213">Authentication request is redirected through the IdP.</span><span class="sxs-lookup"><span data-stu-id="02e26-213">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="02e26-214">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="02e26-214">**Automatic Selection**</span></span>
   
    <span data-ttu-id="02e26-215">If SSO is not active, the system sends the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="02e26-215">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="02e26-216">If SSO is active, the system checks whether the employee has a password.</span><span class="sxs-lookup"><span data-stu-id="02e26-216">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="02e26-217">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="02e26-217">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="02e26-218">However, if the employee has no password, only the SSO URL is sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="02e26-218">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="02e26-219">k.</span><span class="sxs-lookup"><span data-stu-id="02e26-219">k.</span></span> <span data-ttu-id="02e26-220">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="02e26-220">Save your changes.</span></span>

6. <span data-ttu-id="02e26-221">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02e26-221">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="02e26-223">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="02e26-223">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02e26-225">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02e26-225">Creating an Azure AD test user</span></span>
<span data-ttu-id="02e26-226">In this section, you create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02e26-226">In this section, you create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="02e26-228">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02e26-228">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02e26-229">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02e26-229">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="02e26-231">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="02e26-231">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="02e26-232">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="02e26-232">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02e26-234">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="02e26-234">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="02e26-236">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-236">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="02e26-238">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-238">a.</span></span> <span data-ttu-id="02e26-239">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="02e26-239">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="02e26-240">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-240">b.</span></span> <span data-ttu-id="02e26-241">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02e26-241">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="02e26-242">c.</span><span class="sxs-lookup"><span data-stu-id="02e26-242">c.</span></span> <span data-ttu-id="02e26-243">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02e26-243">Click **Next**.</span></span>

6. <span data-ttu-id="02e26-244">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="02e26-244">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_06.png)</span></span> 
   
    <span data-ttu-id="02e26-245">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-245">a.</span></span> <span data-ttu-id="02e26-246">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="02e26-246">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="02e26-247">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-247">b.</span></span> <span data-ttu-id="02e26-248">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="02e26-248">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="02e26-249">c.</span><span class="sxs-lookup"><span data-stu-id="02e26-249">c.</span></span> <span data-ttu-id="02e26-250">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="02e26-250">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="02e26-251">d.</span><span class="sxs-lookup"><span data-stu-id="02e26-251">d.</span></span> <span data-ttu-id="02e26-252">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="02e26-252">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="02e26-253">e.</span><span class="sxs-lookup"><span data-stu-id="02e26-253">e.</span></span> <span data-ttu-id="02e26-254">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02e26-254">Click **Next**.</span></span>

7. <span data-ttu-id="02e26-255">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="02e26-255">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="02e26-257">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02e26-257">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="02e26-259">a.</span><span class="sxs-lookup"><span data-stu-id="02e26-259">a.</span></span> <span data-ttu-id="02e26-260">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="02e26-260">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="02e26-261">b.</span><span class="sxs-lookup"><span data-stu-id="02e26-261">b.</span></span> <span data-ttu-id="02e26-262">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="02e26-262">Click **Complete**.</span></span>   

### <a name="creating-an-sap-cloud-for-customer-test-user"></a><span data-ttu-id="02e26-263">Creating an SAP Cloud for Customer test user</span><span class="sxs-lookup"><span data-stu-id="02e26-263">Creating an SAP Cloud for Customer test user</span></span>
<span data-ttu-id="02e26-264">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="02e26-264">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="02e26-265">Please work with SAP Cloud for Customer support team to add the users in the SAP Cloud for Customer platform.</span><span class="sxs-lookup"><span data-stu-id="02e26-265">Please work with SAP Cloud for Customer support team to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="02e26-266">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span><span class="sxs-lookup"><span data-stu-id="02e26-266">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02e26-267">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02e26-267">Assigning the Azure AD test user</span></span>
<span data-ttu-id="02e26-268">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="02e26-268">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP Cloud for Customer.</span></span>

![Assign User][200] 

<span data-ttu-id="02e26-270">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02e26-270">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="02e26-271">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="02e26-271">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="02e26-273">In the applications list, select **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="02e26-273">In the applications list, select **SAP Cloud for Customer**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_sapcloudforcustomer_50.png) 

3. <span data-ttu-id="02e26-275">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="02e26-275">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="02e26-277">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="02e26-277">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="02e26-278">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="02e26-278">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="02e26-280">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="02e26-280">Testing single sign-on</span></span>
<span data-ttu-id="02e26-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="02e26-281">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="02e26-282">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span><span class="sxs-lookup"><span data-stu-id="02e26-282">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02e26-283">Additional resources</span><span class="sxs-lookup"><span data-stu-id="02e26-283">Additional resources</span></span>
* [<span data-ttu-id="02e26-284">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02e26-284">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02e26-285">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02e26-285">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapcloudforcustomer-tutorial/tutorial_general_205.png































