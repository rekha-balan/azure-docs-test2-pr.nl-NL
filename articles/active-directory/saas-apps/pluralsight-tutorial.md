---
title: 'Tutorial: Azure Active Directory integration with Pluralsight | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pluralsight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: jeedes
ms.openlocfilehash: 81f7e6f7610eb855bd4df1eaf45c6d016befc133
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864515"
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="b4386-103">Tutorial: Azure Active Directory integration with Pluralsight</span><span class="sxs-lookup"><span data-stu-id="b4386-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="b4386-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4386-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4386-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b4386-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b4386-106">You can control in Azure AD who has access to Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="b4386-106">You can control in Azure AD who has access to Pluralsight.</span></span>
- <span data-ttu-id="b4386-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b4386-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b4386-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4386-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b4386-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b4386-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4386-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4386-110">Prerequisites</span></span>

<span data-ttu-id="b4386-111">To configure Azure AD integration with Pluralsight, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b4386-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="b4386-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b4386-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4386-113">A Pluralsight single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b4386-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4386-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b4386-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4386-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b4386-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4386-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b4386-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4386-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4386-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4386-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b4386-118">Scenario description</span></span>
<span data-ttu-id="b4386-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b4386-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4386-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4386-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4386-121">Adding Pluralsight from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4386-121">Adding Pluralsight from the gallery</span></span>
1. <span data-ttu-id="b4386-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4386-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="b4386-123">Adding Pluralsight from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4386-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="b4386-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b4386-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b4386-125">**To add Pluralsight from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4386-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b4386-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b4386-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="b4386-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b4386-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b4386-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b4386-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="b4386-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b4386-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="b4386-133">In the search box, type **Pluralsight**, select **Pluralsight** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b4386-133">In the search box, type **Pluralsight**, select **Pluralsight** from result panel then click **Add** button to add the application.</span></span>

    ![Pluralsight in the results list](./media/pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4386-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4386-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b4386-136">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4386-136">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4386-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4386-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="b4386-138">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b4386-138">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="b4386-139">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b4386-139">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b4386-140">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4386-140">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b4386-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b4386-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b4386-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4386-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b4386-143">**[Create a Pluralsight test user](#create-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b4386-143">**[Create a Pluralsight test user](#create-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b4386-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b4386-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b4386-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b4386-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4386-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4386-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b4386-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="b4386-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="b4386-148">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4386-148">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="b4386-149">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b4386-149">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="b4386-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b4386-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

1. <span data-ttu-id="b4386-153">On the **Pluralsight Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4386-153">On the **Pluralsight Domain and URLs** section, perform the following steps:</span></span>

    ![Pluralsight Domain and URLs single sign-on information](./media/pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="b4386-155">a.</span><span class="sxs-lookup"><span data-stu-id="b4386-155">a.</span></span> <span data-ttu-id="b4386-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.pluralsight.com/sso/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b4386-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.pluralsight.com/sso/<companyname>`</span></span>

    <span data-ttu-id="b4386-157">b.</span><span class="sxs-lookup"><span data-stu-id="b4386-157">b.</span></span> <span data-ttu-id="b4386-158">In the **Identifier** textbox, type the URL: `www.pluralsight.com`</span><span class="sxs-lookup"><span data-stu-id="b4386-158">In the **Identifier** textbox, type the URL: `www.pluralsight.com`</span></span>

    <span data-ttu-id="b4386-159">c.</span><span class="sxs-lookup"><span data-stu-id="b4386-159">c.</span></span> <span data-ttu-id="b4386-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.pluralsight.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="b4386-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.pluralsight.com/sp/ACS.saml2`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b4386-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b4386-161">These values are not real.</span></span> <span data-ttu-id="b4386-162">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="b4386-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b4386-163">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b4386-163">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get these values.</span></span> 

1. <span data-ttu-id="b4386-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b4386-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

1. <span data-ttu-id="b4386-166">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="b4386-166">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="b4386-167">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="b4386-167">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b4386-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="b4386-168">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="b4386-170">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span><span class="sxs-lookup"><span data-stu-id="b4386-170">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="b4386-171">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span><span class="sxs-lookup"><span data-stu-id="b4386-171">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

1. <span data-ttu-id="b4386-172">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4386-172">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="b4386-173">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="b4386-173">Attribute Name</span></span> | <span data-ttu-id="b4386-174">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="b4386-174">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="b4386-175">First Name</span><span class="sxs-lookup"><span data-stu-id="b4386-175">First Name</span></span> |<span data-ttu-id="b4386-176">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b4386-176">user.givenname</span></span> |
   | <span data-ttu-id="b4386-177">Last Name</span><span class="sxs-lookup"><span data-stu-id="b4386-177">Last Name</span></span> |<span data-ttu-id="b4386-178">user.surname</span><span class="sxs-lookup"><span data-stu-id="b4386-178">user.surname</span></span> |
   | <span data-ttu-id="b4386-179">Email</span><span class="sxs-lookup"><span data-stu-id="b4386-179">Email</span></span> |<span data-ttu-id="b4386-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="b4386-180">user.mail</span></span> |
   
   <span data-ttu-id="b4386-181">a.</span><span class="sxs-lookup"><span data-stu-id="b4386-181">a.</span></span> <span data-ttu-id="b4386-182">Click **add user attribute** to open the **Add User Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="b4386-182">Click **add user attribute** to open the **Add User Attribute** dialog.</span></span>
    
     ![Configure Single Sign-On](./media/pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="b4386-184">b.</span><span class="sxs-lookup"><span data-stu-id="b4386-184">b.</span></span> <span data-ttu-id="b4386-185">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b4386-185">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="b4386-186">c.</span><span class="sxs-lookup"><span data-stu-id="b4386-186">c.</span></span> <span data-ttu-id="b4386-187">From the **Attribute Value** list, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b4386-187">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="b4386-188">d.</span><span class="sxs-lookup"><span data-stu-id="b4386-188">d.</span></span> <span data-ttu-id="b4386-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="b4386-189">Click **Ok**.</span></span>    

1. <span data-ttu-id="b4386-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b4386-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/pluralsight-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b4386-192">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="b4386-192">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="b4386-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="b4386-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b4386-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b4386-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b4386-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4386-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4386-196">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4386-196">Create an Azure AD test user</span></span>

<span data-ttu-id="b4386-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4386-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b4386-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4386-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b4386-200">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b4386-200">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/pluralsight-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="b4386-202">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b4386-202">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/pluralsight-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="b4386-204">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b4386-204">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/pluralsight-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="b4386-206">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4386-206">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/pluralsight-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b4386-208">a.</span><span class="sxs-lookup"><span data-stu-id="b4386-208">a.</span></span> <span data-ttu-id="b4386-209">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4386-209">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4386-210">b.</span><span class="sxs-lookup"><span data-stu-id="b4386-210">b.</span></span> <span data-ttu-id="b4386-211">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4386-211">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b4386-212">c.</span><span class="sxs-lookup"><span data-stu-id="b4386-212">c.</span></span> <span data-ttu-id="b4386-213">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b4386-213">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b4386-214">d.</span><span class="sxs-lookup"><span data-stu-id="b4386-214">d.</span></span> <span data-ttu-id="b4386-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b4386-215">Click **Create**.</span></span>
 
### <a name="create-a-pluralsight-test-user"></a><span data-ttu-id="b4386-216">Create a Pluralsight test user</span><span class="sxs-lookup"><span data-stu-id="b4386-216">Create a Pluralsight test user</span></span>

<span data-ttu-id="b4386-217">The objective of this section is to create a user called Britta Simon in Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="b4386-217">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="b4386-218">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span><span class="sxs-lookup"><span data-stu-id="b4386-218">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b4386-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4386-219">Assign the Azure AD test user</span></span>

<span data-ttu-id="b4386-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="b4386-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b4386-222">**To assign Britta Simon to Pluralsight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4386-222">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="b4386-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b4386-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="b4386-225">In the applications list, select **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="b4386-225">In the applications list, select **Pluralsight**.</span></span>

    ![The Pluralsight link in the Applications list](./media/pluralsight-tutorial/tutorial_pluralsight_app.png)  

1. <span data-ttu-id="b4386-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b4386-227">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="b4386-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b4386-229">Click **Add** button.</span></span> <span data-ttu-id="b4386-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b4386-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="b4386-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b4386-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b4386-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b4386-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b4386-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b4386-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b4386-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4386-235">Test single sign-on</span></span>

<span data-ttu-id="b4386-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b4386-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b4386-237">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="b4386-237">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span>
<span data-ttu-id="b4386-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4386-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4386-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b4386-239">Additional resources</span></span>

* [<span data-ttu-id="b4386-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4386-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b4386-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4386-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/pluralsight-tutorial/tutorial_general_203.png

