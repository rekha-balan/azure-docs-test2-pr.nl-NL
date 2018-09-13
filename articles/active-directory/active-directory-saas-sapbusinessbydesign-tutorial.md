---
title: 'Tutorial: Azure Active Directory integration with SAP Business ByDesign | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP Business ByDesign.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 2340da207cf6109a30a6140b6606724b7f3b3bd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661538"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="60c0f-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="60c0f-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>
<span data-ttu-id="60c0f-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60c0f-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60c0f-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="60c0f-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="60c0f-106">You can control in Azure AD who has access to SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="60c0f-106">You can control in Azure AD who has access to SAP Business ByDesign</span></span>
* <span data-ttu-id="60c0f-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="60c0f-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="60c0f-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="60c0f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="60c0f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60c0f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60c0f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="60c0f-110">Prerequisites</span></span>
<span data-ttu-id="60c0f-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="60c0f-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

* <span data-ttu-id="60c0f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="60c0f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="60c0f-113">A SAP Business ByDesign single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="60c0f-113">A SAP Business ByDesign single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60c0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="60c0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="60c0f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="60c0f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="60c0f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="60c0f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="60c0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60c0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60c0f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="60c0f-118">Scenario description</span></span>
<span data-ttu-id="60c0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="60c0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="60c0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="60c0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60c0f-121">Adding SAP Business ByDesign from the gallery</span><span class="sxs-lookup"><span data-stu-id="60c0f-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="60c0f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60c0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="60c0f-123">Adding SAP Business ByDesign from the gallery</span><span class="sxs-lookup"><span data-stu-id="60c0f-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="60c0f-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="60c0f-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60c0f-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60c0f-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60c0f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="60c0f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="60c0f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="60c0f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="60c0f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="60c0f-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="60c0f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="60c0f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="60c0f-135">In the search box, type **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-135">In the search box, type **SAP Business ByDesign**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_01.png)

7. <span data-ttu-id="60c0f-137">In the results pane, select **SAP Business ByDesign**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="60c0f-137">In the results pane, select **SAP Business ByDesign**, and then click **Complete** to add the application.</span></span>
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60c0f-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60c0f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60c0f-140">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60c0f-140">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60c0f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60c0f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="60c0f-142">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span><span class="sxs-lookup"><span data-stu-id="60c0f-142">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="60c0f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="60c0f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP Business ByDesign.</span></span>

<span data-ttu-id="60c0f-144">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="60c0f-144">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60c0f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="60c0f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60c0f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60c0f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60c0f-147">**[Creating a SAP Business ByDesign test user](#creating-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="60c0f-147">**[Creating a SAP Business ByDesign test user](#creating-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="60c0f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60c0f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60c0f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="60c0f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60c0f-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60c0f-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="60c0f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP Business ByDesign application.</span><span class="sxs-lookup"><span data-stu-id="60c0f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="60c0f-152">SAP Business ByDesign application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="60c0f-152">SAP Business ByDesign application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="60c0f-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="60c0f-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="60c0f-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="60c0f-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="60c0f-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="60c0f-155">The following screenshot shows an example for this.</span></span> 

<span data-ttu-id="60c0f-156">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60c0f-156">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="60c0f-157">In the Azure classic portal, on the **SAP Business ByDesign** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-157">In the Azure classic portal, on the **SAP Business ByDesign** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_80.png) 

2. <span data-ttu-id="60c0f-159">In the attributes SAML token attributes list, select the nameidentifier attribute, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-159">In the attributes SAML token attributes list, select the nameidentifier attribute, and then click **Edit**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_84.png) 

3. <span data-ttu-id="60c0f-161">On the Edit User Attribute dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-161">On the Edit User Attribute dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_85.png) 
   
    <span data-ttu-id="60c0f-163">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-163">a.</span></span> <span data-ttu-id="60c0f-164">From the Attribute Value list, select the **ExtractMailPrefix()** fuction</span><span class="sxs-lookup"><span data-stu-id="60c0f-164">From the Attribute Value list, select the **ExtractMailPrefix()** fuction</span></span>
   
    <span data-ttu-id="60c0f-165">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-165">b.</span></span> <span data-ttu-id="60c0f-166">From the Mail list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="60c0f-166">From the Mail list, select the user attribute you want to use for your implementation.</span></span> 
    <span data-ttu-id="60c0f-167">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-167">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span> 
   
    <span data-ttu-id="60c0f-168">c.</span><span class="sxs-lookup"><span data-stu-id="60c0f-168">c.</span></span> <span data-ttu-id="60c0f-169">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-169">Click **Complete**.</span></span> 

4. <span data-ttu-id="60c0f-170">In the classic portal, on the **SAP Business ByDesign** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="60c0f-170">In the classic portal, on the **SAP Business ByDesign** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

5. <span data-ttu-id="60c0f-172">On the **How would you like users to sign on to SAP Business ByDesign** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-172">On the **How would you like users to sign on to SAP Business ByDesign** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_03.png) 

6. <span data-ttu-id="60c0f-174">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-174">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_04.png) 
   
    <span data-ttu-id="60c0f-176">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-176">a.</span></span> <span data-ttu-id="60c0f-177">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP Business ByDesign application using the following pattern: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="60c0f-177">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP Business ByDesign application using the following pattern: `https://<servername>.sapbydesign.com`</span></span>
   
    <span data-ttu-id="60c0f-178">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-178">b.</span></span> <span data-ttu-id="60c0f-179">click **Next**</span><span class="sxs-lookup"><span data-stu-id="60c0f-179">click **Next**</span></span>
7. <span data-ttu-id="60c0f-180">On the **Configure single sign-on at SAP Business ByDesign** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-180">On the **Configure single sign-on at SAP Business ByDesign** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_05.png)
   
    <span data-ttu-id="60c0f-182">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-182">a.</span></span> <span data-ttu-id="60c0f-183">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="60c0f-183">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="60c0f-184">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-184">b.</span></span> <span data-ttu-id="60c0f-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-185">Click **Next**.</span></span>
8. <span data-ttu-id="60c0f-186">To get SSO configured for your application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-186">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="60c0f-187">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-187">a.</span></span> <span data-ttu-id="60c0f-188">Sign on to your SAP Business ByDesign portal with administrator rights.</span><span class="sxs-lookup"><span data-stu-id="60c0f-188">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="60c0f-189">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-189">b.</span></span> <span data-ttu-id="60c0f-190">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="60c0f-190">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="60c0f-191">c.</span><span class="sxs-lookup"><span data-stu-id="60c0f-191">c.</span></span> <span data-ttu-id="60c0f-192">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="60c0f-192">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure classic portal.</span></span> <span data-ttu-id="60c0f-193">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span><span class="sxs-lookup"><span data-stu-id="60c0f-193">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="60c0f-195">d.</span><span class="sxs-lookup"><span data-stu-id="60c0f-195">d.</span></span> <span data-ttu-id="60c0f-196">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-196">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="60c0f-197">e.</span><span class="sxs-lookup"><span data-stu-id="60c0f-197">e.</span></span> <span data-ttu-id="60c0f-198">Click **Activate Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-198">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="60c0f-199">f.</span><span class="sxs-lookup"><span data-stu-id="60c0f-199">f.</span></span> <span data-ttu-id="60c0f-200">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="60c0f-200">Save your changes.</span></span>
   
    <span data-ttu-id="60c0f-201">g.</span><span class="sxs-lookup"><span data-stu-id="60c0f-201">g.</span></span> <span data-ttu-id="60c0f-202">Click the **My System** tab.</span><span class="sxs-lookup"><span data-stu-id="60c0f-202">Click the **My System** tab.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="60c0f-204">h.</span><span class="sxs-lookup"><span data-stu-id="60c0f-204">h.</span></span> <span data-ttu-id="60c0f-205">Copy the **SSO URL** and paste it into the **Azure AD Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="60c0f-205">Copy the **SSO URL** and paste it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="60c0f-207">i.</span><span class="sxs-lookup"><span data-stu-id="60c0f-207">i.</span></span> <span data-ttu-id="60c0f-208">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-208">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="60c0f-209">j.</span><span class="sxs-lookup"><span data-stu-id="60c0f-209">j.</span></span> <span data-ttu-id="60c0f-210">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span><span class="sxs-lookup"><span data-stu-id="60c0f-210">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="60c0f-211">In the URL Sent to Employee dropdown list, you can choose between the following options:</span><span class="sxs-lookup"><span data-stu-id="60c0f-211">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="60c0f-212">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="60c0f-212">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="60c0f-213">The system sends only the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="60c0f-213">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="60c0f-214">The employee cannot log on using SSO, and must use password or certificate instead.</span><span class="sxs-lookup"><span data-stu-id="60c0f-214">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="60c0f-215">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="60c0f-215">**SSO URL**</span></span> 
   
    <span data-ttu-id="60c0f-216">The system sends only the SSO URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="60c0f-216">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="60c0f-217">The employee can log on using SSO.</span><span class="sxs-lookup"><span data-stu-id="60c0f-217">The employee can log on using SSO.</span></span> <span data-ttu-id="60c0f-218">Authentication request is redirected through the IdP.</span><span class="sxs-lookup"><span data-stu-id="60c0f-218">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="60c0f-219">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="60c0f-219">**Automatic Selection**</span></span>
   
    <span data-ttu-id="60c0f-220">If SSO is not active, the system sends the normal system URL to the employee.</span><span class="sxs-lookup"><span data-stu-id="60c0f-220">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="60c0f-221">If SSO is active, the system checks whether the employee has a password.</span><span class="sxs-lookup"><span data-stu-id="60c0f-221">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="60c0f-222">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="60c0f-222">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="60c0f-223">However, if the employee has no password, only the SSO URL is sent to the employee.</span><span class="sxs-lookup"><span data-stu-id="60c0f-223">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="60c0f-224">k.</span><span class="sxs-lookup"><span data-stu-id="60c0f-224">k.</span></span> <span data-ttu-id="60c0f-225">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="60c0f-225">Save your changes.</span></span>

9. <span data-ttu-id="60c0f-226">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-226">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

10. <span data-ttu-id="60c0f-228">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-228">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60c0f-230">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60c0f-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="60c0f-231">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60c0f-231">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="60c0f-233">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60c0f-233">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60c0f-234">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-234">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="60c0f-236">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="60c0f-236">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="60c0f-237">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-237">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60c0f-239">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-239">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="60c0f-241">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-241">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="60c0f-243">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-243">a.</span></span> <span data-ttu-id="60c0f-244">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="60c0f-244">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="60c0f-245">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-245">b.</span></span> <span data-ttu-id="60c0f-246">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-246">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="60c0f-247">c.</span><span class="sxs-lookup"><span data-stu-id="60c0f-247">c.</span></span> <span data-ttu-id="60c0f-248">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-248">Click **Next**.</span></span>

6. <span data-ttu-id="60c0f-249">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-249">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="60c0f-251">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-251">a.</span></span> <span data-ttu-id="60c0f-252">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-252">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="60c0f-253">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-253">b.</span></span> <span data-ttu-id="60c0f-254">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-254">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="60c0f-255">c.</span><span class="sxs-lookup"><span data-stu-id="60c0f-255">c.</span></span> <span data-ttu-id="60c0f-256">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-256">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="60c0f-257">d.</span><span class="sxs-lookup"><span data-stu-id="60c0f-257">d.</span></span> <span data-ttu-id="60c0f-258">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-258">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="60c0f-259">e.</span><span class="sxs-lookup"><span data-stu-id="60c0f-259">e.</span></span> <span data-ttu-id="60c0f-260">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-260">Click **Next**.</span></span>

7. <span data-ttu-id="60c0f-261">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-261">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="60c0f-263">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60c0f-263">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="60c0f-265">a.</span><span class="sxs-lookup"><span data-stu-id="60c0f-265">a.</span></span> <span data-ttu-id="60c0f-266">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-266">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="60c0f-267">b.</span><span class="sxs-lookup"><span data-stu-id="60c0f-267">b.</span></span> <span data-ttu-id="60c0f-268">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-268">Click **Complete**.</span></span>   

### <a name="creating-an-sap-business-bydesign-test-user"></a><span data-ttu-id="60c0f-269">Creating an SAP Business ByDesign test user</span><span class="sxs-lookup"><span data-stu-id="60c0f-269">Creating an SAP Business ByDesign test user</span></span>
<span data-ttu-id="60c0f-270">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="60c0f-270">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="60c0f-271">Please work with SAP Business ByDesign support team to add the users in the SAP Business ByDesign platform.</span><span class="sxs-lookup"><span data-stu-id="60c0f-271">Please work with SAP Business ByDesign support team to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="60c0f-272">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span><span class="sxs-lookup"><span data-stu-id="60c0f-272">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60c0f-273">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60c0f-273">Assigning the Azure AD test user</span></span>
<span data-ttu-id="60c0f-274">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="60c0f-274">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP Business ByDesign.</span></span>

![Assign User][200] 

<span data-ttu-id="60c0f-276">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60c0f-276">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="60c0f-277">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="60c0f-277">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="60c0f-279">In the applications list, select **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-279">In the applications list, select **SAP Business ByDesign**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_50.png) 

3. <span data-ttu-id="60c0f-281">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-281">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="60c0f-283">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-283">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="60c0f-284">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="60c0f-284">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="60c0f-286">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="60c0f-286">Testing single sign-on</span></span>
<span data-ttu-id="60c0f-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="60c0f-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60c0f-288">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span><span class="sxs-lookup"><span data-stu-id="60c0f-288">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60c0f-289">Additional resources</span><span class="sxs-lookup"><span data-stu-id="60c0f-289">Additional resources</span></span>
* [<span data-ttu-id="60c0f-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60c0f-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60c0f-291">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60c0f-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_205.png































