---
title: 'Tutorial: Azure Active Directory integration with Cisco Webex | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cisco Webex.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2018
ms.author: jeedes
ms.openlocfilehash: 73e20afdcacec76482f8ebf01bf2cef2105912a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871296"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="29e98-103">Tutorial: Azure Active Directory integration with Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="29e98-103">Tutorial: Azure Active Directory integration with Cisco Webex</span></span>

<span data-ttu-id="29e98-104">In this tutorial, you learn how to integrate Cisco Webex with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29e98-104">In this tutorial, you learn how to integrate Cisco Webex with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29e98-105">Integrating Cisco Webex with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="29e98-105">Integrating Cisco Webex with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29e98-106">You can control in Azure AD who has access to Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="29e98-106">You can control in Azure AD who has access to Cisco Webex.</span></span>
- <span data-ttu-id="29e98-107">You can enable your users to automatically get signed in to Cisco Webex with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="29e98-107">You can enable your users to automatically get signed in to Cisco Webex with their Azure AD accounts.</span></span>
- <span data-ttu-id="29e98-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="29e98-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="29e98-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="29e98-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29e98-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="29e98-110">Prerequisites</span></span>

<span data-ttu-id="29e98-111">To configure Azure AD integration with Cisco Webex, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="29e98-111">To configure Azure AD integration with Cisco Webex, you need the following items:</span></span>

- <span data-ttu-id="29e98-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="29e98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29e98-113">A Cisco Webex single sign-on-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="29e98-113">A Cisco Webex single sign-on-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29e98-114">We don't recommend using a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="29e98-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="29e98-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="29e98-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="29e98-116">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="29e98-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="29e98-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29e98-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29e98-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="29e98-118">Scenario description</span></span>
<span data-ttu-id="29e98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="29e98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29e98-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="29e98-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29e98-121">Adding Cisco Webex from the gallery</span><span class="sxs-lookup"><span data-stu-id="29e98-121">Adding Cisco Webex from the gallery</span></span>
2. <span data-ttu-id="29e98-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="29e98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-cisco-webex-from-the-gallery"></a><span data-ttu-id="29e98-123">Add Cisco Webex from the gallery</span><span class="sxs-lookup"><span data-stu-id="29e98-123">Add Cisco Webex from the gallery</span></span>
<span data-ttu-id="29e98-124">To configure the integration of Cisco Webex into Azure AD, you need to add Cisco Webex from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="29e98-124">To configure the integration of Cisco Webex into Azure AD, you need to add Cisco Webex from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29e98-125">**To add Cisco Webex from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29e98-125">**To add Cisco Webex from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="29e98-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="29e98-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="29e98-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="29e98-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="29e98-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="29e98-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="29e98-131">To add a new application, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="29e98-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="29e98-133">In the search box, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="29e98-133">In the search box, type **Cisco Webex**.</span></span> 

5. <span data-ttu-id="29e98-134">Select **Cisco Webex** from the results panel.</span><span class="sxs-lookup"><span data-stu-id="29e98-134">Select **Cisco Webex** from the results panel.</span></span> <span data-ttu-id="29e98-135">Then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="29e98-135">Then select the **Add** button to add the application.</span></span>

    ![Cisco Webex in the results list](./media/cisco-webex-tutorial/tutorial_ciscowebex_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29e98-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="29e98-137">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29e98-138">In this section, you configure and test Azure AD single sign-on with Cisco Webex based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="29e98-138">In this section, you configure and test Azure AD single sign-on with Cisco Webex based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29e98-139">For single sign-on to work, Azure AD needs to know who the counterpart user in Cisco Webex is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29e98-139">For single sign-on to work, Azure AD needs to know who the counterpart user in Cisco Webex is to a user in Azure AD.</span></span> <span data-ttu-id="29e98-140">In other words, you need to establish a link between an Azure AD user and a related user in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="29e98-140">In other words, you need to establish a link between an Azure AD user and a related user in Cisco Webex.</span></span>

<span data-ttu-id="29e98-141">In Cisco Webex, give the value **Username** the same value as **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29e98-141">In Cisco Webex, give the value **Username** the same value as **user name** in Azure AD.</span></span> <span data-ttu-id="29e98-142">Now you have established the link between the two users.</span><span class="sxs-lookup"><span data-stu-id="29e98-142">Now you have established the link between the two users.</span></span> 

<span data-ttu-id="29e98-143">To configure and test Azure AD single sign-on with Cisco Webex, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="29e98-143">To configure and test Azure AD single sign-on with Cisco Webex, complete the following building blocks:</span></span>

1. <span data-ttu-id="29e98-144">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="29e98-144">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29e98-145">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29e98-145">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29e98-146">[Create a Cisco Webex test user](#create-a-cisco-webex-test-user) to have a counterpart of Britta Simon in Cisco Webex that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="29e98-146">[Create a Cisco Webex test user](#create-a-cisco-webex-test-user) to have a counterpart of Britta Simon in Cisco Webex that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29e98-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="29e98-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29e98-148">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="29e98-148">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29e98-149">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="29e98-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29e98-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Webex application.</span><span class="sxs-lookup"><span data-stu-id="29e98-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Webex application.</span></span>

<span data-ttu-id="29e98-151">**To configure Azure AD single sign-on with Cisco Webex, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29e98-151">**To configure Azure AD single sign-on with Cisco Webex, take the following steps:**</span></span>

1. <span data-ttu-id="29e98-152">In the Azure portal, on the **Cisco Webex** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="29e98-152">In the Azure portal, on the **Cisco Webex** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="29e98-154">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="29e98-154">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Single sign-on dialog box](./media/cisco-webex-tutorial/tutorial_ciscowebex_samlbase.png)

3. <span data-ttu-id="29e98-156">In a different web browser window, sign in to your Cisco Webex company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="29e98-156">In a different web browser window, sign in to your Cisco Webex company site as an administrator.</span></span>

4. <span data-ttu-id="29e98-157">Click **Settings** from the left of the menu.</span><span class="sxs-lookup"><span data-stu-id="29e98-157">Click **Settings** from the left of the menu.</span></span>

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_cisco_webex_10.png)

5. <span data-ttu-id="29e98-159">On the settings page scroll down under the **Authentication** section, click **Modify**.</span><span class="sxs-lookup"><span data-stu-id="29e98-159">On the settings page scroll down under the **Authentication** section, click **Modify**.</span></span>

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_cisco_webex_14.png)

6. <span data-ttu-id="29e98-161">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span><span class="sxs-lookup"><span data-stu-id="29e98-161">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_cisco_webex_15.png)

7. <span data-ttu-id="29e98-163">On the **Export Directory Metadata** page, click **Download Metadata File** to download the metadata file.</span><span class="sxs-lookup"><span data-stu-id="29e98-163">On the **Export Directory Metadata** page, click **Download Metadata File** to download the metadata file.</span></span>

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_cisco_webex_16.png)

8. <span data-ttu-id="29e98-165">In the Azure portal, under the **Cisco Webex Domain and URLs** section, upload the downloaded **Service Provider metadata file** and configure the application by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="29e98-165">In the Azure portal, under the **Cisco Webex Domain and URLs** section, upload the downloaded **Service Provider metadata file** and configure the application by performing the following steps:</span></span>

    <span data-ttu-id="29e98-166">a.</span><span class="sxs-lookup"><span data-stu-id="29e98-166">a.</span></span> <span data-ttu-id="29e98-167">Click **Upload metadata file**.</span><span class="sxs-lookup"><span data-stu-id="29e98-167">Click **Upload metadata file**.</span></span>

    ![Cisco Webex Domain and URLs single sign-on information](./media/cisco-webex-tutorial/tutorial_ciscowebex_upload.png)

    <span data-ttu-id="29e98-169">b.</span><span class="sxs-lookup"><span data-stu-id="29e98-169">b.</span></span> <span data-ttu-id="29e98-170">Click on **folder logo** to select the metadata file and click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="29e98-170">Click on **folder logo** to select the metadata file and click **Upload**.</span></span>

    ![Cisco Webex Domain and URLs single sign-on information](./media/cisco-webex-tutorial/tutorial_ciscowebex_uploadconfig.png)

    <span data-ttu-id="29e98-172">c.</span><span class="sxs-lookup"><span data-stu-id="29e98-172">c.</span></span> <span data-ttu-id="29e98-173">After successful completion of uploading **Service Provider metadata file** the **Identifier** and **Reply URL** values get auto populated in **Cisco Webex Domain and URLs** section textbox as shown below:</span><span class="sxs-lookup"><span data-stu-id="29e98-173">After successful completion of uploading **Service Provider metadata file** the **Identifier** and **Reply URL** values get auto populated in **Cisco Webex Domain and URLs** section textbox as shown below:</span></span>

    ![Cisco Webex Domain and URLs single sign-on information](./media/cisco-webex-tutorial/tutorial_ciscowebex_url.png)

    <span data-ttu-id="29e98-175">d.</span><span class="sxs-lookup"><span data-stu-id="29e98-175">d.</span></span> <span data-ttu-id="29e98-176">In the **Sign-on URL** box, type a URL with the following pattern: `https://<SUBDOMAIN>.webex.com/`</span><span class="sxs-lookup"><span data-stu-id="29e98-176">In the **Sign-on URL** box, type a URL with the following pattern: `https://<SUBDOMAIN>.webex.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="29e98-177">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="29e98-177">These values are not real.</span></span> <span data-ttu-id="29e98-178">Update these values with the actual Sign on URL.</span><span class="sxs-lookup"><span data-stu-id="29e98-178">Update these values with the actual Sign on URL.</span></span> <span data-ttu-id="29e98-179">Contact [Cisco Webex Client support team](https://www.webex.co.in/support/support-overview.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="29e98-179">Contact [Cisco Webex Client support team](https://www.webex.co.in/support/support-overview.html) to get these values.</span></span>

9. <span data-ttu-id="29e98-180">Cisco Webex application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="29e98-180">Cisco Webex application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="29e98-181">Configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="29e98-181">Configure the following attributes  for this application.</span></span> <span data-ttu-id="29e98-182">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="29e98-182">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="29e98-183">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="29e98-183">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_ciscowebex_07.png) 

10. <span data-ttu-id="29e98-185">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="29e98-185">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    |  <span data-ttu-id="29e98-186">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="29e98-186">Attribute Name</span></span>  | <span data-ttu-id="29e98-187">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="29e98-187">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="29e98-188">firstname</span><span class="sxs-lookup"><span data-stu-id="29e98-188">firstname</span></span>    | <span data-ttu-id="29e98-189">user.givenname</span><span class="sxs-lookup"><span data-stu-id="29e98-189">user.givenname</span></span> |
    |   <span data-ttu-id="29e98-190">lastname</span><span class="sxs-lookup"><span data-stu-id="29e98-190">lastname</span></span>    | <span data-ttu-id="29e98-191">user.surname</span><span class="sxs-lookup"><span data-stu-id="29e98-191">user.surname</span></span> |
    |   <span data-ttu-id="29e98-192">uid</span><span class="sxs-lookup"><span data-stu-id="29e98-192">uid</span></span>    | <span data-ttu-id="29e98-193">user.mail</span><span class="sxs-lookup"><span data-stu-id="29e98-193">user.mail</span></span> |

    <span data-ttu-id="29e98-194">a.</span><span class="sxs-lookup"><span data-stu-id="29e98-194">a.</span></span> <span data-ttu-id="29e98-195">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="29e98-195">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="29e98-198">b.</span><span class="sxs-lookup"><span data-stu-id="29e98-198">b.</span></span> <span data-ttu-id="29e98-199">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="29e98-199">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="29e98-200">c.</span><span class="sxs-lookup"><span data-stu-id="29e98-200">c.</span></span> <span data-ttu-id="29e98-201">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="29e98-201">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="29e98-202">d.</span><span class="sxs-lookup"><span data-stu-id="29e98-202">d.</span></span> <span data-ttu-id="29e98-203">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="29e98-203">Click **Ok**.</span></span>

11. <span data-ttu-id="29e98-204">On the **SAML Signing Certificate** section, select **Metadata XML**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="29e98-204">On the **SAML Signing Certificate** section, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/cisco-webex-tutorial/tutorial_ciscowebex_certificate.png) 

12. <span data-ttu-id="29e98-206">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="29e98-206">Select **Save**.</span></span>

    ![Configure the single sign-On Save button](./media/cisco-webex-tutorial/tutorial_general_400.png)
    
13. <span data-ttu-id="29e98-208">On the Cisco Webex company site administrator page, use the file browser option to locate and upload the Azure AD metadata file.</span><span class="sxs-lookup"><span data-stu-id="29e98-208">On the Cisco Webex company site administrator page, use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="29e98-209">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and go to next screen.</span><span class="sxs-lookup"><span data-stu-id="29e98-209">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and go to next screen.</span></span> 

    ![Configure Single Sign-On](./media/cisco-webex-tutorial/tutorial_cisco_webex_11.png)

14. <span data-ttu-id="29e98-211">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span><span class="sxs-lookup"><span data-stu-id="29e98-211">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

15. <span data-ttu-id="29e98-212">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="29e98-212">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29e98-213">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="29e98-213">Create an Azure AD test user</span></span>

<span data-ttu-id="29e98-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29e98-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="29e98-216">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29e98-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29e98-217">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="29e98-217">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/cisco-webex-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29e98-219">To display the list of users, go to **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="29e98-219">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/cisco-webex-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29e98-221">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="29e98-221">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/cisco-webex-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29e98-223">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="29e98-223">In the **User** dialog box, take the following steps:</span></span>

    ![The User dialog box](./media/cisco-webex-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29e98-225">a.</span><span class="sxs-lookup"><span data-stu-id="29e98-225">a.</span></span> <span data-ttu-id="29e98-226">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29e98-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29e98-227">b.</span><span class="sxs-lookup"><span data-stu-id="29e98-227">b.</span></span> <span data-ttu-id="29e98-228">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29e98-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="29e98-229">c.</span><span class="sxs-lookup"><span data-stu-id="29e98-229">c.</span></span> <span data-ttu-id="29e98-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="29e98-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="29e98-231">d.</span><span class="sxs-lookup"><span data-stu-id="29e98-231">d.</span></span> <span data-ttu-id="29e98-232">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="29e98-232">Select **Create**.</span></span>
 
### <a name="create-a-cisco-webex-test-user"></a><span data-ttu-id="29e98-233">Create a Cisco Webex test user</span><span class="sxs-lookup"><span data-stu-id="29e98-233">Create a Cisco Webex test user</span></span>

<span data-ttu-id="29e98-234">The objective of this section is to create a user called Britta Simon in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="29e98-234">The objective of this section is to create a user called Britta Simon in Cisco Webex.</span></span> <span data-ttu-id="29e98-235">Cisco Webex supports just-in-time provisioning and automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="29e98-235">Cisco Webex supports just-in-time provisioning and automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="29e98-236">You can find more details [here](https://docs.microsoft.com/azure/active-directory/saas-apps/cisco-webex-provisioning-tutorial) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="29e98-236">You can find more details [here](https://docs.microsoft.com/azure/active-directory/saas-apps/cisco-webex-provisioning-tutorial) on how to configure automatic user provisioning.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29e98-237">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="29e98-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="29e98-238">In this section, you enable the user Britta Simon to use Azure single sign-on by granting them access to Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="29e98-238">In this section, you enable the user Britta Simon to use Azure single sign-on by granting them access to Cisco Webex.</span></span>

![Assign the user role][200] 

<span data-ttu-id="29e98-240">**To assign Britta Simon to Cisco Webex, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29e98-240">**To assign Britta Simon to Cisco Webex, take the following steps:**</span></span>

1. <span data-ttu-id="29e98-241">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="29e98-241">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="29e98-242">Next, go to the directory view, and then to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="29e98-242">Next, go to the directory view, and then to **Enterprise applications**.</span></span>  

2. <span data-ttu-id="29e98-243">Select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="29e98-243">Select **All applications**.</span></span>

    ![Assign user][201] 

3. <span data-ttu-id="29e98-245">In the applications list, select **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="29e98-245">In the applications list, select **Cisco Webex**.</span></span>

    ![The Cisco Webex link in the Applications list](./media/cisco-webex-tutorial/tutorial_ciscowebex_app.png)  

3. <span data-ttu-id="29e98-247">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="29e98-247">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="29e98-249">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="29e98-249">Select the **Add** button.</span></span> <span data-ttu-id="29e98-250">Then select **Users and groups** in the  **Add Assignment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="29e98-250">Then select **Users and groups** in the  **Add Assignment** dialog box.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="29e98-252">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span><span class="sxs-lookup"><span data-stu-id="29e98-252">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span></span>

6. <span data-ttu-id="29e98-253">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="29e98-253">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="29e98-254">Select the **Assign** button in the **Add Assignment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="29e98-254">Select the **Assign** button in the **Add Assignment** dialog box.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29e98-255">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="29e98-255">Test single sign-on</span></span>

<span data-ttu-id="29e98-256">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="29e98-256">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="29e98-257">When you select the Cisco Webex tile in the access panel, you automatically get signed in to your Cisco Webex application.</span><span class="sxs-lookup"><span data-stu-id="29e98-257">When you select the Cisco Webex tile in the access panel, you automatically get signed in to your Cisco Webex application.</span></span>

<span data-ttu-id="29e98-258">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29e98-258">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29e98-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="29e98-259">Additional resources</span></span>

* [<span data-ttu-id="29e98-260">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29e98-260">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="29e98-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29e98-261">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cisco-webex-tutorial/tutorial_general_01.png
[2]: ./media/cisco-webex-tutorial/tutorial_general_02.png
[3]: ./media/cisco-webex-tutorial/tutorial_general_03.png
[4]: ./media/cisco-webex-tutorial/tutorial_general_04.png

[100]: ./media/cisco-webex-tutorial/tutorial_general_100.png

[200]: ./media/cisco-webex-tutorial/tutorial_general_200.png
[201]: ./media/cisco-webex-tutorial/tutorial_general_201.png
[202]: ./media/cisco-webex-tutorial/tutorial_general_202.png
[203]: ./media/cisco-webex-tutorial/tutorial_general_203.png

