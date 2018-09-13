---
title: 'Tutorial: Azure Active Directory integration with LinkedIn Learning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LinkedIn Learning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: 02e7d9d26b389e82365f3447cceb5566244236f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870969"
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="ae73f-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="ae73f-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="ae73f-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae73f-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae73f-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ae73f-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae73f-106">You can control in Azure AD who has access to LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="ae73f-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="ae73f-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ae73f-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae73f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae73f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae73f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ae73f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae73f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae73f-110">Prerequisites</span></span>

<span data-ttu-id="ae73f-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ae73f-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="ae73f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ae73f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae73f-113">A LinkedIn Learning single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ae73f-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae73f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ae73f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae73f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ae73f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae73f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ae73f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae73f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae73f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae73f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ae73f-118">Scenario description</span></span>
<span data-ttu-id="ae73f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ae73f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae73f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae73f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae73f-121">Adding LinkedIn Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae73f-121">Adding LinkedIn Learning from the gallery</span></span>
1. <span data-ttu-id="ae73f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae73f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="ae73f-123">Adding LinkedIn Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae73f-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="ae73f-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ae73f-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae73f-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae73f-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae73f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ae73f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae73f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ae73f-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ae73f-133">In the search box, type **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="ae73f-134">From results panel, click **LinkedIn Learning** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae73f-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae73f-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae73f-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae73f-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae73f-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae73f-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae73f-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="ae73f-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ae73f-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="ae73f-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="ae73f-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="ae73f-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae73f-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae73f-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ae73f-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ae73f-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ae73f-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ae73f-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae73f-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ae73f-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ae73f-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae73f-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae73f-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae73f-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span><span class="sxs-lookup"><span data-stu-id="ae73f-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="ae73f-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae73f-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="ae73f-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ae73f-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae73f-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial-linkedin_01.png)

1. <span data-ttu-id="ae73f-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ae73f-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

1. <span data-ttu-id="ae73f-155">In **Account Center**, click **Global Settings** under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="ae73f-156">Also, select **Learning - Default** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="ae73f-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

1. <span data-ttu-id="ae73f-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="ae73f-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

1. <span data-ttu-id="ae73f-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span><span class="sxs-lookup"><span data-stu-id="ae73f-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="ae73f-162">a.</span><span class="sxs-lookup"><span data-stu-id="ae73f-162">a.</span></span> <span data-ttu-id="ae73f-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="ae73f-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="ae73f-164">b.</span><span class="sxs-lookup"><span data-stu-id="ae73f-164">b.</span></span> <span data-ttu-id="ae73f-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="ae73f-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

1. <span data-ttu-id="ae73f-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span><span class="sxs-lookup"><span data-stu-id="ae73f-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
1. <span data-ttu-id="ae73f-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="ae73f-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ae73f-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="ae73f-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ae73f-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="ae73f-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="ae73f-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="ae73f-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/updateusermail.png)
    
1. <span data-ttu-id="ae73f-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span><span class="sxs-lookup"><span data-stu-id="ae73f-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="ae73f-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span><span class="sxs-lookup"><span data-stu-id="ae73f-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="ae73f-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ae73f-175">Attribute Name</span></span> | <span data-ttu-id="ae73f-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ae73f-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ae73f-177">email</span><span class="sxs-lookup"><span data-stu-id="ae73f-177">email</span></span>| <span data-ttu-id="ae73f-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="ae73f-178">user.mail</span></span> |    
    | <span data-ttu-id="ae73f-179">department</span><span class="sxs-lookup"><span data-stu-id="ae73f-179">department</span></span>| <span data-ttu-id="ae73f-180">user.department</span><span class="sxs-lookup"><span data-stu-id="ae73f-180">user.department</span></span> |
    | <span data-ttu-id="ae73f-181">firstname</span><span class="sxs-lookup"><span data-stu-id="ae73f-181">firstname</span></span>| <span data-ttu-id="ae73f-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ae73f-182">user.givenname</span></span> |
    | <span data-ttu-id="ae73f-183">lastname</span><span class="sxs-lookup"><span data-stu-id="ae73f-183">lastname</span></span>| <span data-ttu-id="ae73f-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="ae73f-184">user.surname</span></span> |
    
    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="ae73f-186">a.</span><span class="sxs-lookup"><span data-stu-id="ae73f-186">a.</span></span> <span data-ttu-id="ae73f-187">Click **Add Attribute** to open the attribute dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/tutorial_attribute_04.png)

    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ae73f-190">b.</span><span class="sxs-lookup"><span data-stu-id="ae73f-190">b.</span></span> <span data-ttu-id="ae73f-191">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ae73f-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ae73f-192">c.</span><span class="sxs-lookup"><span data-stu-id="ae73f-192">c.</span></span> <span data-ttu-id="ae73f-193">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ae73f-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ae73f-194">d.</span><span class="sxs-lookup"><span data-stu-id="ae73f-194">d.</span></span> <span data-ttu-id="ae73f-195">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="ae73f-195">Click **Ok**</span></span>

1. <span data-ttu-id="ae73f-196">Perform the following steps on the **name** attribute-</span><span class="sxs-lookup"><span data-stu-id="ae73f-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="ae73f-197">a.</span><span class="sxs-lookup"><span data-stu-id="ae73f-197">a.</span></span> <span data-ttu-id="ae73f-198">Click on the attribute to open the **Edit Attribute** window.</span><span class="sxs-lookup"><span data-stu-id="ae73f-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/url_update.png)

    <span data-ttu-id="ae73f-200">b.</span><span class="sxs-lookup"><span data-stu-id="ae73f-200">b.</span></span> <span data-ttu-id="ae73f-201">Delete the URL value from the **namespace**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="ae73f-202">c.</span><span class="sxs-lookup"><span data-stu-id="ae73f-202">c.</span></span> <span data-ttu-id="ae73f-203">Click **Ok** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="ae73f-203">Click **Ok** to save the setting.</span></span>

1. <span data-ttu-id="ae73f-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ae73f-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png)

1. <span data-ttu-id="ae73f-206">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-206">Click **Save**.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ae73f-208">Go to **LinkedIn Admin Settings** section.</span><span class="sxs-lookup"><span data-stu-id="ae73f-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="ae73f-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span><span class="sxs-lookup"><span data-stu-id="ae73f-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

1. <span data-ttu-id="ae73f-211">Click **On** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="ae73f-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="ae73f-212">SSO status changes from **Not Connected** to **Connected**</span><span class="sxs-lookup"><span data-stu-id="ae73f-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae73f-214">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae73f-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae73f-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ae73f-217">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae73f-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae73f-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ae73f-220">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ae73f-222">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="ae73f-224">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae73f-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae73f-226">a.</span><span class="sxs-lookup"><span data-stu-id="ae73f-226">a.</span></span> <span data-ttu-id="ae73f-227">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae73f-228">b.</span><span class="sxs-lookup"><span data-stu-id="ae73f-228">b.</span></span> <span data-ttu-id="ae73f-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae73f-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae73f-230">c.</span><span class="sxs-lookup"><span data-stu-id="ae73f-230">c.</span></span> <span data-ttu-id="ae73f-231">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae73f-232">d.</span><span class="sxs-lookup"><span data-stu-id="ae73f-232">d.</span></span> <span data-ttu-id="ae73f-233">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-233">Click **Create**.</span></span>

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="ae73f-234">Creating a LinkedIn Learning test user</span><span class="sxs-lookup"><span data-stu-id="ae73f-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="ae73f-235">LinkedIn Learning Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="ae73f-235">LinkedIn Learning Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="ae73f-236">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active Just in time provisioning and this will also assign a license to the user.</span><span class="sxs-lookup"><span data-stu-id="ae73f-236">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Creating an Azure AD test user](./media/linkedinlearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae73f-238">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae73f-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae73f-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="ae73f-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Assign User][200] 

<span data-ttu-id="ae73f-241">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae73f-241">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="ae73f-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="ae73f-244">In the applications list, select **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-244">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configure Single Sign-On](./media/linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png)

1. <span data-ttu-id="ae73f-246">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ae73f-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="ae73f-248">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ae73f-248">Click **Add** button.</span></span> <span data-ttu-id="ae73f-249">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ae73f-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ae73f-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ae73f-252">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-252">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ae73f-253">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae73f-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ae73f-254">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae73f-254">Testing single sign-on</span></span>

<span data-ttu-id="ae73f-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae73f-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae73f-256">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span><span class="sxs-lookup"><span data-stu-id="ae73f-256">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae73f-257">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ae73f-257">Additional resources</span></span>

* [<span data-ttu-id="ae73f-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae73f-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ae73f-259">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae73f-259">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/linkedinlearning-tutorial/tutorial_general_203.png
