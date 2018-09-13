---
title: 'Tutorial: Azure Active Directory integration with Qlik Sense Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Qlik Sense Enterprise.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: ad43094a6444b830ff29a3ab610bb2dd3567c3b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552936"
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="721db-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="721db-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>
<span data-ttu-id="721db-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="721db-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="721db-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="721db-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="721db-106">You can control in Azure AD who has access to Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="721db-106">You can control in Azure AD who has access to Qlik Sense Enterprise</span></span>
* <span data-ttu-id="721db-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="721db-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="721db-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="721db-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="721db-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="721db-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="721db-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="721db-110">Prerequisites</span></span>
<span data-ttu-id="721db-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="721db-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

* <span data-ttu-id="721db-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="721db-112">An Azure AD subscription</span></span>
* <span data-ttu-id="721db-113">A Qlik Sense Enterprise single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="721db-113">A Qlik Sense Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="721db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="721db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="721db-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="721db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="721db-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="721db-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="721db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="721db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="721db-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="721db-118">Scenario description</span></span>
<span data-ttu-id="721db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="721db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="721db-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="721db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="721db-121">Adding Qlik Sense Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="721db-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="721db-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="721db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="721db-123">Adding Qlik Sense Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="721db-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="721db-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="721db-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="721db-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="721db-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="721db-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="721db-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="721db-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="721db-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="721db-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="721db-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="721db-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="721db-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="721db-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="721db-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="721db-135">In the search box, type **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="721db-135">In the search box, type **Qlik Sense Enterprise**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_01.png)

7. <span data-ttu-id="721db-137">In the results pane, select **Qlik Sense Enterprise**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="721db-137">In the results pane, select **Qlik Sense Enterprise**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="721db-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="721db-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="721db-140">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="721db-140">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="721db-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="721db-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="721db-142">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="721db-142">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="721db-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="721db-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Qlik Sense Enterprise.</span></span>

<span data-ttu-id="721db-144">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="721db-144">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="721db-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="721db-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="721db-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="721db-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="721db-147">**[Creating a Qlik Sense Enterprise test user](#creating-a-qliksense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="721db-147">**[Creating a Qlik Sense Enterprise test user](#creating-a-qliksense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="721db-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="721db-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="721db-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="721db-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="721db-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="721db-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="721db-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Qlik Sense Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="721db-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="721db-152">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="721db-152">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="721db-153">In the classic portal, on the **Qlik Sense Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="721db-153">In the classic portal, on the **Qlik Sense Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="721db-155">On the **How would you like users to sign on to Qlik Sense Enterprise** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="721db-155">On the **How would you like users to sign on to Qlik Sense Enterprise** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_03.png) 

3. <span data-ttu-id="721db-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="721db-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_04.png) 
   
    <span data-ttu-id="721db-159">a.</span><span class="sxs-lookup"><span data-stu-id="721db-159">a.</span></span> <span data-ttu-id="721db-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Qlik Sense Enterprise application using the following pattern: **https://\<Qlik Sense Fully Qualifed Hostname\>:443/<Virtual Proxy Prefix\>/samlauthn/**.</span><span class="sxs-lookup"><span data-stu-id="721db-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Qlik Sense Enterprise application using the following pattern: **https://\<Qlik Sense Fully Qualifed Hostname\>:443/<Virtual Proxy Prefix\>/samlauthn/**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="721db-161">Note the trailing slash at the end of this URI.</span><span class="sxs-lookup"><span data-stu-id="721db-161">Note the trailing slash at the end of this URI.</span></span>  <span data-ttu-id="721db-162">It is required.</span><span class="sxs-lookup"><span data-stu-id="721db-162">It is required.</span></span>
    > 
    > 
   
    <span data-ttu-id="721db-163">b.</span><span class="sxs-lookup"><span data-stu-id="721db-163">b.</span></span> <span data-ttu-id="721db-164">click **Next**</span><span class="sxs-lookup"><span data-stu-id="721db-164">click **Next**</span></span>

4. <span data-ttu-id="721db-165">On the **Configure single sign-on at Qlik Sense Enterprise** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="721db-165">On the **Configure single sign-on at Qlik Sense Enterprise** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_05.png)
   
    <span data-ttu-id="721db-167">a.</span><span class="sxs-lookup"><span data-stu-id="721db-167">a.</span></span> <span data-ttu-id="721db-168">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="721db-168">Click **Download metadata**, and then save the file on your computer.</span></span>  <span data-ttu-id="721db-169">Be prepared to edit this metadata file before uploading to the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-169">Be prepared to edit this metadata file before uploading to the Qlik Sense server.</span></span>
   
    <span data-ttu-id="721db-170">b.</span><span class="sxs-lookup"><span data-stu-id="721db-170">b.</span></span> <span data-ttu-id="721db-171">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="721db-171">Click **Next**.</span></span>

5. <span data-ttu-id="721db-172">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-172">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="721db-173">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-173">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    > 
    > 
   
    ![QlikSense][qs24]
   
    <span data-ttu-id="721db-175">a.</span><span class="sxs-lookup"><span data-stu-id="721db-175">a.</span></span> <span data-ttu-id="721db-176">Open the FederationMetaData.xml file downloaded from Azure in a text editor.</span><span class="sxs-lookup"><span data-stu-id="721db-176">Open the FederationMetaData.xml file downloaded from Azure in a text editor.</span></span>
   
    <span data-ttu-id="721db-177">b.</span><span class="sxs-lookup"><span data-stu-id="721db-177">b.</span></span> <span data-ttu-id="721db-178">Search for the value **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="721db-178">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="721db-179">There will be four entries (two pairs of opening and closing element tags).</span><span class="sxs-lookup"><span data-stu-id="721db-179">There will be four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="721db-180">c.</span><span class="sxs-lookup"><span data-stu-id="721db-180">c.</span></span> <span data-ttu-id="721db-181">Delete the RoleDescriptor tags and all information in between from the file.</span><span class="sxs-lookup"><span data-stu-id="721db-181">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="721db-182">d.</span><span class="sxs-lookup"><span data-stu-id="721db-182">d.</span></span> <span data-ttu-id="721db-183">Save the file and keep it nearby for use later in this document.</span><span class="sxs-lookup"><span data-stu-id="721db-183">Save the file and keep it nearby for use later in this document.</span></span>
6. <span data-ttu-id="721db-184">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span><span class="sxs-lookup"><span data-stu-id="721db-184">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>
7. <span data-ttu-id="721db-185">In the QMC, click on the Virtual Proxy menu item.</span><span class="sxs-lookup"><span data-stu-id="721db-185">In the QMC, click on the Virtual Proxy menu item.</span></span>
   
    ![QlikSense][qs6] 
8. <span data-ttu-id="721db-187">At the bottom of the screen, click the Create new button.</span><span class="sxs-lookup"><span data-stu-id="721db-187">At the bottom of the screen, click the Create new button.</span></span>
   
    ![QlikSense][qs7]
9. <span data-ttu-id="721db-189">The Virtual proxy edit screen appears.</span><span class="sxs-lookup"><span data-stu-id="721db-189">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="721db-190">On the right side of the screen is a menu for making configuration options visible.</span><span class="sxs-lookup"><span data-stu-id="721db-190">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]
10. <span data-ttu-id="721db-192">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-192">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="721db-194">a.</span><span class="sxs-lookup"><span data-stu-id="721db-194">a.</span></span> <span data-ttu-id="721db-195">The Description field is a friendly name for the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-195">The Description field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="721db-196">Enter a value for a description.</span><span class="sxs-lookup"><span data-stu-id="721db-196">Enter a value for a description.</span></span>
    
    <span data-ttu-id="721db-197">b.</span><span class="sxs-lookup"><span data-stu-id="721db-197">b.</span></span> <span data-ttu-id="721db-198">The Prefix field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="721db-198">The Prefix field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="721db-199">Enter a unique prefix name for this virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="721db-199">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="721db-200">c.</span><span class="sxs-lookup"><span data-stu-id="721db-200">c.</span></span> <span data-ttu-id="721db-201">Session inactivity timeout (minutes) is the timeout for connections through this virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="721db-201">Session inactivity timeout (minutes) is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="721db-202">d.</span><span class="sxs-lookup"><span data-stu-id="721db-202">d.</span></span> <span data-ttu-id="721db-203">The Session cookie header name is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="721db-203">The Session cookie header name is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="721db-204">This name must be unique.</span><span class="sxs-lookup"><span data-stu-id="721db-204">This name must be unique.</span></span>
11. <span data-ttu-id="721db-205">Click on the Authentication menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="721db-205">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="721db-206">The Authentication screen appears.</span><span class="sxs-lookup"><span data-stu-id="721db-206">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="721db-208">a.</span><span class="sxs-lookup"><span data-stu-id="721db-208">a.</span></span> <span data-ttu-id="721db-209">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="721db-209">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="721db-210">The default option is No anonymous user.</span><span class="sxs-lookup"><span data-stu-id="721db-210">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="721db-211">b.</span><span class="sxs-lookup"><span data-stu-id="721db-211">b.</span></span> <span data-ttu-id="721db-212">The **Authentication method** drop down determines the authentication scheme the virtual proxy will use.</span><span class="sxs-lookup"><span data-stu-id="721db-212">The **Authentication method** drop down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="721db-213">Select SAML from the drop down list.</span><span class="sxs-lookup"><span data-stu-id="721db-213">Select SAML from the drop down list.</span></span>  <span data-ttu-id="721db-214">More options will appear as a result.</span><span class="sxs-lookup"><span data-stu-id="721db-214">More options will appear as a result.</span></span>
    
    <span data-ttu-id="721db-215">c.</span><span class="sxs-lookup"><span data-stu-id="721db-215">c.</span></span> <span data-ttu-id="721db-216">In the **SAML host URI field**, input the hostname users will enter to access Qlik Sense through this SAML virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="721db-216">In the **SAML host URI field**, input the hostname users will enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="721db-217">The hostname is the uri of the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-217">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="721db-218">d.</span><span class="sxs-lookup"><span data-stu-id="721db-218">d.</span></span> <span data-ttu-id="721db-219">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span><span class="sxs-lookup"><span data-stu-id="721db-219">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="721db-220">e.</span><span class="sxs-lookup"><span data-stu-id="721db-220">e.</span></span> <span data-ttu-id="721db-221">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="721db-221">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="721db-222">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-222">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="721db-223">**Please refer to the instructions above if the file has yet to be edited.**</span><span class="sxs-lookup"><span data-stu-id="721db-223">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="721db-224">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-224">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="721db-225">f.</span><span class="sxs-lookup"><span data-stu-id="721db-225">f.</span></span> <span data-ttu-id="721db-226">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD will send to the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-226">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD will send to the Qlik Sense server.</span></span>  <span data-ttu-id="721db-227">Schema reference information is available in the Azure app screens post configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-227">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="721db-228">To use the name attribute, **enter http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span><span class="sxs-lookup"><span data-stu-id="721db-228">To use the name attribute, **enter http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**.</span></span>
    
    <span data-ttu-id="721db-229">g.</span><span class="sxs-lookup"><span data-stu-id="721db-229">g.</span></span> <span data-ttu-id="721db-230">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span><span class="sxs-lookup"><span data-stu-id="721db-230">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="721db-231">Hardcoded values must be surrounded by **square brackets []**.</span><span class="sxs-lookup"><span data-stu-id="721db-231">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="721db-232">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span><span class="sxs-lookup"><span data-stu-id="721db-232">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="721db-233">h.</span><span class="sxs-lookup"><span data-stu-id="721db-233">h.</span></span> <span data-ttu-id="721db-234">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-234">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="721db-235">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="721db-235">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="721db-236">i.</span><span class="sxs-lookup"><span data-stu-id="721db-236">i.</span></span> <span data-ttu-id="721db-237">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span><span class="sxs-lookup"><span data-stu-id="721db-237">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>
12. <span data-ttu-id="721db-238">Click on the Load balancing menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="721db-238">Click on the Load balancing menu option to make it visible.</span></span>  <span data-ttu-id="721db-239">The Load Balancing screen appears.</span><span class="sxs-lookup"><span data-stu-id="721db-239">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]
13. <span data-ttu-id="721db-241">Click on the Add new server node button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="721db-241">Click on the Add new server node button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the Add button.</span></span>
    
    ![QlikSense][qs12]
14. <span data-ttu-id="721db-243">Click on the Advanced menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="721db-243">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="721db-244">The Advanced screen appears.</span><span class="sxs-lookup"><span data-stu-id="721db-244">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="721db-246">a.</span><span class="sxs-lookup"><span data-stu-id="721db-246">a.</span></span> <span data-ttu-id="721db-247">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="721db-247">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="721db-248">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span><span class="sxs-lookup"><span data-stu-id="721db-248">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="721db-249">The hostname is the same value as the SAML host uri without the https://.</span><span class="sxs-lookup"><span data-stu-id="721db-249">The hostname is the same value as the SAML host uri without the https://.</span></span>
15. <span data-ttu-id="721db-250">Click the Apply button.</span><span class="sxs-lookup"><span data-stu-id="721db-250">Click the Apply button.</span></span>
    
    ![QlikSense][qs14]
16. <span data-ttu-id="721db-252">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span><span class="sxs-lookup"><span data-stu-id="721db-252">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]
17. <span data-ttu-id="721db-254">On the right side of the screen, the Associated items menu appears.</span><span class="sxs-lookup"><span data-stu-id="721db-254">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="721db-255">Click on the Proxies menu option.</span><span class="sxs-lookup"><span data-stu-id="721db-255">Click on the Proxies menu option.</span></span>
    
    ![QlikSense][qs16]
18. <span data-ttu-id="721db-257">The proxy screen appears.</span><span class="sxs-lookup"><span data-stu-id="721db-257">The proxy screen appears.</span></span>  <span data-ttu-id="721db-258">Click the Link button at the bottom to link a proxy to the virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="721db-258">Click the Link button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]
19. <span data-ttu-id="721db-260">Select the proxy node that will support this virtual proxy connection and click the Link button.</span><span class="sxs-lookup"><span data-stu-id="721db-260">Select the proxy node that will support this virtual proxy connection and click the Link button.</span></span>  <span data-ttu-id="721db-261">After linking, the proxy will be listed under associated proxies.</span><span class="sxs-lookup"><span data-stu-id="721db-261">After linking, the proxy will be listed under associated proxies.</span></span>
    
    <span data-ttu-id="721db-262">![QlikSense][qs18]
    ![QlikSense][qs19]</span><span class="sxs-lookup"><span data-stu-id="721db-262">![QlikSense][qs18]
![QlikSense][qs19]</span></span>
20. <span data-ttu-id="721db-263">After about five to ten seconds, the Refresh QMC message will appear.</span><span class="sxs-lookup"><span data-stu-id="721db-263">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="721db-264">Click the Refresh QMC button.</span><span class="sxs-lookup"><span data-stu-id="721db-264">Click the Refresh QMC button.</span></span>
    
    ![QlikSense][qs20]
21. <span data-ttu-id="721db-266">When the QMC refreshes, click on the Virtual proxies menu item.</span><span class="sxs-lookup"><span data-stu-id="721db-266">When the QMC refreshes, click on the Virtual proxies menu item.</span></span> <span data-ttu-id="721db-267">The new SAML virtual proxy entry is listed in the table on the screen.</span><span class="sxs-lookup"><span data-stu-id="721db-267">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="721db-268">Single click on the virtual proxy entry.</span><span class="sxs-lookup"><span data-stu-id="721db-268">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]
22. <span data-ttu-id="721db-270">At the bottom of the screen, the Download SP metadata button will activate.</span><span class="sxs-lookup"><span data-stu-id="721db-270">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="721db-271">Click the Download SP metadata button to save the metadata to a file.</span><span class="sxs-lookup"><span data-stu-id="721db-271">Click the Download SP metadata button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]
23. <span data-ttu-id="721db-273">Open the sp metadata file.</span><span class="sxs-lookup"><span data-stu-id="721db-273">Open the sp metadata file.</span></span>  <span data-ttu-id="721db-274">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span><span class="sxs-lookup"><span data-stu-id="721db-274">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="721db-275">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span><span class="sxs-lookup"><span data-stu-id="721db-275">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="721db-276">If they are not matching then you should replace them in the Azure AD App configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="721db-276">If they are not matching then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]
24. <span data-ttu-id="721db-278">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="721db-278">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]
25. <span data-ttu-id="721db-280">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="721db-280">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="721db-282">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="721db-282">Creating an Azure AD test user</span></span>
<span data-ttu-id="721db-283">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="721db-283">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="721db-285">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="721db-285">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="721db-286">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="721db-286">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="721db-288">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="721db-288">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="721db-289">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="721db-289">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="721db-291">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="721db-291">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="721db-293">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="721db-293">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_05.png)</span></span> 
   
    <span data-ttu-id="721db-294">a.</span><span class="sxs-lookup"><span data-stu-id="721db-294">a.</span></span> <span data-ttu-id="721db-295">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="721db-295">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="721db-296">b.</span><span class="sxs-lookup"><span data-stu-id="721db-296">b.</span></span> <span data-ttu-id="721db-297">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="721db-297">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="721db-298">c.</span><span class="sxs-lookup"><span data-stu-id="721db-298">c.</span></span> <span data-ttu-id="721db-299">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="721db-299">Click **Next**.</span></span>

6. <span data-ttu-id="721db-300">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="721db-300">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="721db-302">a.</span><span class="sxs-lookup"><span data-stu-id="721db-302">a.</span></span> <span data-ttu-id="721db-303">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="721db-303">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="721db-304">b.</span><span class="sxs-lookup"><span data-stu-id="721db-304">b.</span></span> <span data-ttu-id="721db-305">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="721db-305">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="721db-306">c.</span><span class="sxs-lookup"><span data-stu-id="721db-306">c.</span></span> <span data-ttu-id="721db-307">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="721db-307">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="721db-308">d.</span><span class="sxs-lookup"><span data-stu-id="721db-308">d.</span></span> <span data-ttu-id="721db-309">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="721db-309">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="721db-310">e.</span><span class="sxs-lookup"><span data-stu-id="721db-310">e.</span></span> <span data-ttu-id="721db-311">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="721db-311">Click **Next**.</span></span>

7. <span data-ttu-id="721db-312">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="721db-312">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="721db-314">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="721db-314">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="721db-316">a.</span><span class="sxs-lookup"><span data-stu-id="721db-316">a.</span></span> <span data-ttu-id="721db-317">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="721db-317">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="721db-318">b.</span><span class="sxs-lookup"><span data-stu-id="721db-318">b.</span></span> <span data-ttu-id="721db-319">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="721db-319">Click **Complete**.</span></span>   

### <a name="creating-an-qlik-sense-enterprise-test-user"></a><span data-ttu-id="721db-320">Creating an Qlik Sense Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="721db-320">Creating an Qlik Sense Enterprise test user</span></span>
<span data-ttu-id="721db-321">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="721db-321">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="721db-322">Please work with Qlik Sense Enterprise support team to add the users in the Qlik Sense Enterprise platform.</span><span class="sxs-lookup"><span data-stu-id="721db-322">Please work with Qlik Sense Enterprise support team to add the users in the Qlik Sense Enterprise platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="721db-323">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="721db-323">Assigning the Azure AD test user</span></span>
<span data-ttu-id="721db-324">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="721db-324">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Qlik Sense Enterprise.</span></span>

![Assign User][200] 

<span data-ttu-id="721db-326">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="721db-326">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="721db-327">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="721db-327">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="721db-329">In the applications list, select **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="721db-329">In the applications list, select **Qlik Sense Enterprise**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_50.png) 

3. <span data-ttu-id="721db-331">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="721db-331">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="721db-333">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="721db-333">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="721db-334">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="721db-334">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

## <a name="testing-single-sign-on"></a><span data-ttu-id="721db-336">Testing single sign-On</span><span class="sxs-lookup"><span data-stu-id="721db-336">Testing single sign-On</span></span>
<span data-ttu-id="721db-337">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="721db-337">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="721db-338">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="721db-338">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="721db-339">Additional resources</span><span class="sxs-lookup"><span data-stu-id="721db-339">Additional resources</span></span>
* [<span data-ttu-id="721db-340">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="721db-340">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="721db-341">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="721db-341">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_205.png

[qs6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_21.png
[qs22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_22.png
[qs23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_23.png
[qs24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_25.png
[qs26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_26.png
[qs51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

















































