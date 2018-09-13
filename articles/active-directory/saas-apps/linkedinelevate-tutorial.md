---
title: 'Tutorial: Azure Active Directory integration with LinkedIn Elevate | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LinkedIn Elevate.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: f8f12263ca71b8e88033484bc03fc4cff9e25bc8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864438"
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="f5918-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="f5918-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="f5918-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5918-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5918-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f5918-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5918-106">You can control in Azure AD who has access to LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="f5918-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="f5918-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f5918-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5918-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="f5918-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f5918-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f5918-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5918-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5918-110">Prerequisites</span></span>

<span data-ttu-id="f5918-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f5918-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="f5918-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f5918-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5918-113">A LinkedIn Elevate single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f5918-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5918-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f5918-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5918-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f5918-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5918-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f5918-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f5918-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5918-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5918-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f5918-118">Scenario description</span></span>
<span data-ttu-id="f5918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f5918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="f5918-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f5918-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5918-121">Adding LinkedIn Elevate from the gallery</span><span class="sxs-lookup"><span data-stu-id="f5918-121">Adding LinkedIn Elevate from the gallery</span></span>
1. <span data-ttu-id="f5918-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5918-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="f5918-123">Adding LinkedIn Elevate from the gallery</span><span class="sxs-lookup"><span data-stu-id="f5918-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="f5918-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f5918-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5918-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5918-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5918-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f5918-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![Active Directory][1]

1. <span data-ttu-id="f5918-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f5918-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5918-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f5918-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="f5918-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f5918-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f5918-133">In the search box, type **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="f5918-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="f5918-134">From results panel, click **LinkedIn Elevate** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f5918-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5918-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5918-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5918-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5918-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5918-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5918-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="f5918-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f5918-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="f5918-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="f5918-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="f5918-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f5918-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5918-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f5918-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f5918-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5918-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f5918-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5918-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f5918-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f5918-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f5918-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f5918-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5918-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5918-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5918-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span><span class="sxs-lookup"><span data-stu-id="f5918-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="f5918-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5918-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="f5918-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f5918-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f5918-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="f5918-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial-linkedin_01.png)

1. <span data-ttu-id="f5918-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f5918-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

1. <span data-ttu-id="f5918-155">In **Account Center**, click **Global Settings** under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f5918-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="f5918-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="f5918-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_admin_01.png)

1. <span data-ttu-id="f5918-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="f5918-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_admin_03.png)

1. <span data-ttu-id="f5918-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span><span class="sxs-lookup"><span data-stu-id="f5918-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="f5918-162">a.</span><span class="sxs-lookup"><span data-stu-id="f5918-162">a.</span></span> <span data-ttu-id="f5918-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="f5918-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="f5918-164">b.</span><span class="sxs-lookup"><span data-stu-id="f5918-164">b.</span></span> <span data-ttu-id="f5918-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="f5918-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

1. <span data-ttu-id="f5918-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span><span class="sxs-lookup"><span data-stu-id="f5918-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_signon_02.png) 

1. <span data-ttu-id="f5918-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="f5918-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="f5918-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="f5918-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="f5918-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="f5918-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="f5918-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="f5918-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/updateusermail.png)

1. <span data-ttu-id="f5918-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span><span class="sxs-lookup"><span data-stu-id="f5918-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="f5918-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span><span class="sxs-lookup"><span data-stu-id="f5918-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="f5918-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="f5918-175">Attribute Name</span></span> | <span data-ttu-id="f5918-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="f5918-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f5918-177">department</span><span class="sxs-lookup"><span data-stu-id="f5918-177">department</span></span>| <span data-ttu-id="f5918-178">user.department</span><span class="sxs-lookup"><span data-stu-id="f5918-178">user.department</span></span> |

      ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/userattribute.png)

      <span data-ttu-id="f5918-180">a.</span><span class="sxs-lookup"><span data-stu-id="f5918-180">a.</span></span> <span data-ttu-id="f5918-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span><span class="sxs-lookup"><span data-stu-id="f5918-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/adduserattribute.png)

      <span data-ttu-id="f5918-183">b.</span><span class="sxs-lookup"><span data-stu-id="f5918-183">b.</span></span> <span data-ttu-id="f5918-184">Click on **Ok** to save the attribute.</span><span class="sxs-lookup"><span data-stu-id="f5918-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="f5918-185">c.</span><span class="sxs-lookup"><span data-stu-id="f5918-185">c.</span></span> <span data-ttu-id="f5918-186">Change the name of the attribute **emailaddress** to **email**.</span><span class="sxs-lookup"><span data-stu-id="f5918-186">Change the name of the attribute **emailaddress** to **email**.</span></span>

1. <span data-ttu-id="f5918-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f5918-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial-linkedinElevate_certificate.png) 

1. <span data-ttu-id="f5918-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5918-189">Click **Save**.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f5918-191">Go to **LinkedIn Admin Settings** section.</span><span class="sxs-lookup"><span data-stu-id="f5918-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="f5918-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span><span class="sxs-lookup"><span data-stu-id="f5918-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_metadata_03.png)

1. <span data-ttu-id="f5918-194">Click **On** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="f5918-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="f5918-195">SSO status will change from **Not Connected** to **Connected**</span><span class="sxs-lookup"><span data-stu-id="f5918-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5918-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f5918-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5918-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5918-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f5918-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5918-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5918-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f5918-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f5918-203">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="f5918-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>

    ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f5918-205">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5918-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>

    ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f5918-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5918-207">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5918-209">a.</span><span class="sxs-lookup"><span data-stu-id="f5918-209">a.</span></span> <span data-ttu-id="f5918-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5918-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5918-211">b.</span><span class="sxs-lookup"><span data-stu-id="f5918-211">b.</span></span> <span data-ttu-id="f5918-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5918-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5918-213">c.</span><span class="sxs-lookup"><span data-stu-id="f5918-213">c.</span></span> <span data-ttu-id="f5918-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f5918-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5918-215">d.</span><span class="sxs-lookup"><span data-stu-id="f5918-215">d.</span></span> <span data-ttu-id="f5918-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5918-216">Click **Create**.</span></span>

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="f5918-217">Creating a LinkedIn Elevate test user</span><span class="sxs-lookup"><span data-stu-id="f5918-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="f5918-218">LinkedIn Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="f5918-218">LinkedIn Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="f5918-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active Just in time provisioning and this will also assign a license to the user.</span><span class="sxs-lookup"><span data-stu-id="f5918-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active Just in time provisioning and this will also assign a license to the user.</span></span> <span data-ttu-id="f5918-220">LinkedIn Elevate also supports automatic user provisioning, you can find more details [here](linkedinelevate-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="f5918-220">LinkedIn Elevate also supports automatic user provisioning, you can find more details [here](linkedinelevate-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

   ![Creating an Azure AD test user](./media/linkedinelevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5918-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f5918-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5918-223">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="f5918-223">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Assign User][200] 

<span data-ttu-id="f5918-225">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5918-225">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="f5918-226">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f5918-226">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="f5918-228">In the applications list, select **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="f5918-228">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Configure Single Sign-On](./media/linkedinelevate-tutorial/tutorial-linkedinElevate_0001.png) 

1. <span data-ttu-id="f5918-230">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f5918-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f5918-232">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f5918-232">Click **Add** button.</span></span> <span data-ttu-id="f5918-233">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5918-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f5918-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f5918-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f5918-236">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5918-236">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f5918-237">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5918-237">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="f5918-238">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5918-238">Testing single sign-on</span></span>

<span data-ttu-id="f5918-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f5918-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5918-240">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span><span class="sxs-lookup"><span data-stu-id="f5918-240">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5918-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f5918-241">Additional resources</span></span>

* [<span data-ttu-id="f5918-242">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5918-242">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="f5918-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5918-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f5918-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5918-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="f5918-245">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="f5918-245">Configure User Provisioning</span></span>](linkedinelevate-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/linkedinElevate-tutorial/tutorial_general_203.png