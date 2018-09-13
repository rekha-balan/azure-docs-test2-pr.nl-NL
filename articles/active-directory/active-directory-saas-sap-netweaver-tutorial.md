---
title: 'Tutorial: Azure Active Directory integration with SAP NetWeaver | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP NetWeaver.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: c86d86b9e7ef6255d533ee79335564cc57b0f27c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553178"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="364a1-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="364a1-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>
<span data-ttu-id="364a1-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="364a1-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory.</span></span>

<span data-ttu-id="364a1-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="364a1-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="364a1-106">You can control in Azure AD who has access to SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="364a1-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
* <span data-ttu-id="364a1-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="364a1-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="364a1-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="364a1-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="364a1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="364a1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="364a1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="364a1-110">Prerequisites</span></span>
<span data-ttu-id="364a1-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="364a1-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

* <span data-ttu-id="364a1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="364a1-112">An Azure AD subscription</span></span>
* <span data-ttu-id="364a1-113">A SAP NetWeaver single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="364a1-113">A SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="364a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="364a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="364a1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="364a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="364a1-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="364a1-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="364a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="364a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="364a1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="364a1-118">Scenario description</span></span>
<span data-ttu-id="364a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="364a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="364a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="364a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="364a1-121">Adding SAP NetWeaver from the gallery</span><span class="sxs-lookup"><span data-stu-id="364a1-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="364a1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="364a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="364a1-123">Adding SAP NetWeaver from the gallery</span><span class="sxs-lookup"><span data-stu-id="364a1-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="364a1-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="364a1-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="364a1-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="364a1-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="364a1-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="364a1-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="364a1-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="364a1-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="364a1-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="364a1-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="364a1-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="364a1-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="364a1-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="364a1-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="364a1-135">In the search box, type **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="364a1-135">In the search box, type **SAP NetWeaver**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_01.png)
7. <span data-ttu-id="364a1-137">In the results pane, select **SAP NetWeaver**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="364a1-137">In the results pane, select **SAP NetWeaver**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="364a1-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="364a1-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="364a1-140">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="364a1-140">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="364a1-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364a1-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="364a1-142">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span><span class="sxs-lookup"><span data-stu-id="364a1-142">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="364a1-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="364a1-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="364a1-144">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="364a1-144">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="364a1-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="364a1-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="364a1-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="364a1-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="364a1-147">**[Creating a SAP NetWeaver test user](#creating-a-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="364a1-147">**[Creating a SAP NetWeaver test user](#creating-a-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="364a1-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="364a1-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="364a1-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="364a1-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="364a1-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="364a1-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="364a1-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP NetWeaver application.</span><span class="sxs-lookup"><span data-stu-id="364a1-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="364a1-152">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="364a1-152">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="364a1-153">In the classic portal, on the **SAP NetWeaver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="364a1-153">In the classic portal, on the **SAP NetWeaver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="364a1-155">On the **How would you like users to sign on to SAP NetWeaver** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="364a1-155">On the **How would you like users to sign on to SAP NetWeaver** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_03.png) 
3. <span data-ttu-id="364a1-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="364a1-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_04.png) 
   
    <span data-ttu-id="364a1-159">a.</span><span class="sxs-lookup"><span data-stu-id="364a1-159">a.</span></span> <span data-ttu-id="364a1-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP NetWeaver application using the following pattern: **https://\<your company instance of SAP NetWeaver\>**.</span><span class="sxs-lookup"><span data-stu-id="364a1-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SAP NetWeaver application using the following pattern: **https://\<your company instance of SAP NetWeaver\>**.</span></span>
   
    <span data-ttu-id="364a1-161">b.</span><span class="sxs-lookup"><span data-stu-id="364a1-161">b.</span></span> <span data-ttu-id="364a1-162">In the **Identifier** textbox, type the URL using the following pattern: **https://\<your company instance of SAP NetWeaver\>**.</span><span class="sxs-lookup"><span data-stu-id="364a1-162">In the **Identifier** textbox, type the URL using the following pattern: **https://\<your company instance of SAP NetWeaver\>**.</span></span>
   
    <span data-ttu-id="364a1-163">c.</span><span class="sxs-lookup"><span data-stu-id="364a1-163">c.</span></span> <span data-ttu-id="364a1-164">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<your company instance of SAP NetWeaver\>/sap/saml2/sp/acs/100**.</span><span class="sxs-lookup"><span data-stu-id="364a1-164">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<your company instance of SAP NetWeaver\>/sap/saml2/sp/acs/100**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="364a1-165">You will able to find all these values in the Federation Metadata doucument provided by your SAP NetWeaver partner.</span><span class="sxs-lookup"><span data-stu-id="364a1-165">You will able to find all these values in the Federation Metadata doucument provided by your SAP NetWeaver partner.</span></span>
    > 
    > 
   
    <span data-ttu-id="364a1-166">d.</span><span class="sxs-lookup"><span data-stu-id="364a1-166">d.</span></span> <span data-ttu-id="364a1-167">click **Next**</span><span class="sxs-lookup"><span data-stu-id="364a1-167">click **Next**</span></span>

4. <span data-ttu-id="364a1-168">On the **Configure single sign-on at SAP NetWeaver** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="364a1-168">On the **Configure single sign-on at SAP NetWeaver** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_05.png)
   
    <span data-ttu-id="364a1-170">a.</span><span class="sxs-lookup"><span data-stu-id="364a1-170">a.</span></span> <span data-ttu-id="364a1-171">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="364a1-171">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="364a1-172">b.</span><span class="sxs-lookup"><span data-stu-id="364a1-172">b.</span></span> <span data-ttu-id="364a1-173">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="364a1-173">Click **Next**.</span></span>
5. <span data-ttu-id="364a1-174">To get SSO configured for your application, contact your SAP NetWeaver partner and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="364a1-174">To get SSO configured for your application, contact your SAP NetWeaver partner and provide them with the following:</span></span>
   
    <span data-ttu-id="364a1-175">• The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="364a1-175">• The downloaded **metadata**</span></span>
   
    <span data-ttu-id="364a1-176">• The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="364a1-176">• The **Entity ID**</span></span>
   
    <span data-ttu-id="364a1-177">• The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="364a1-177">• The **SAML SSO URL**</span></span>
   
    <span data-ttu-id="364a1-178">• The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="364a1-178">• The **Single Sign Out Service URL**</span></span>
6. <span data-ttu-id="364a1-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="364a1-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="364a1-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="364a1-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="364a1-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="364a1-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="364a1-184">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="364a1-184">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="364a1-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="364a1-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="364a1-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="364a1-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="364a1-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="364a1-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="364a1-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="364a1-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="364a1-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="364a1-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="364a1-194">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="364a1-194">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_05.png)</span></span> 
   
    <span data-ttu-id="364a1-195">a.</span><span class="sxs-lookup"><span data-stu-id="364a1-195">a.</span></span> <span data-ttu-id="364a1-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="364a1-196">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="364a1-197">b.</span><span class="sxs-lookup"><span data-stu-id="364a1-197">b.</span></span> <span data-ttu-id="364a1-198">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="364a1-198">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="364a1-199">c.</span><span class="sxs-lookup"><span data-stu-id="364a1-199">c.</span></span> <span data-ttu-id="364a1-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="364a1-200">Click **Next**.</span></span>
6. <span data-ttu-id="364a1-201">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="364a1-201">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_06.png)</span></span> 
   
    <span data-ttu-id="364a1-202">a.</span><span class="sxs-lookup"><span data-stu-id="364a1-202">a.</span></span> <span data-ttu-id="364a1-203">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="364a1-203">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="364a1-204">b.</span><span class="sxs-lookup"><span data-stu-id="364a1-204">b.</span></span> <span data-ttu-id="364a1-205">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="364a1-205">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="364a1-206">c.</span><span class="sxs-lookup"><span data-stu-id="364a1-206">c.</span></span> <span data-ttu-id="364a1-207">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="364a1-207">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="364a1-208">d.</span><span class="sxs-lookup"><span data-stu-id="364a1-208">d.</span></span> <span data-ttu-id="364a1-209">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="364a1-209">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="364a1-210">e.</span><span class="sxs-lookup"><span data-stu-id="364a1-210">e.</span></span> <span data-ttu-id="364a1-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="364a1-211">Click **Next**.</span></span>

7. <span data-ttu-id="364a1-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="364a1-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="364a1-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="364a1-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="364a1-216">a.</span><span class="sxs-lookup"><span data-stu-id="364a1-216">a.</span></span> <span data-ttu-id="364a1-217">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="364a1-217">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="364a1-218">b.</span><span class="sxs-lookup"><span data-stu-id="364a1-218">b.</span></span> <span data-ttu-id="364a1-219">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="364a1-219">Click **Complete**.</span></span>   

### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="364a1-220">Creating an SAP NetWeaver test user</span><span class="sxs-lookup"><span data-stu-id="364a1-220">Creating an SAP NetWeaver test user</span></span>
<span data-ttu-id="364a1-221">In this section, you create a user called Britta Simon in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="364a1-221">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="364a1-222">Please work with your SAP NetWeaver partner to add the users in the SAP NetWeaver platform.</span><span class="sxs-lookup"><span data-stu-id="364a1-222">Please work with your SAP NetWeaver partner to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="364a1-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="364a1-223">Assigning the Azure AD test user</span></span>
<span data-ttu-id="364a1-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="364a1-224">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP NetWeaver.</span></span>

![Assign User][200] 

<span data-ttu-id="364a1-226">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="364a1-226">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="364a1-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="364a1-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="364a1-229">In the applications list, select **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="364a1-229">In the applications list, select **SAP NetWeaver**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_50.png) 
3. <span data-ttu-id="364a1-231">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="364a1-231">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="364a1-233">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="364a1-233">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="364a1-234">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="364a1-234">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="364a1-236">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="364a1-236">Testing Single Sign-On</span></span>
<span data-ttu-id="364a1-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="364a1-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="364a1-238">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span><span class="sxs-lookup"><span data-stu-id="364a1-238">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="364a1-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="364a1-239">Additional resources</span></span>
* [<span data-ttu-id="364a1-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="364a1-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="364a1-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="364a1-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_205.png

























