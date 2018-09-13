---
title: 'Tutorial: Azure Active Directory integration with Adobe Creative Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: c199073f-02ce-45c2-b515-8285d4bbbca2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2018
ms.author: jeedes
ms.openlocfilehash: 506f52faf916aa0d5ca2e8587bdbcc16ab88e130
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869085"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="3565d-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="3565d-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="3565d-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3565d-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3565d-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3565d-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3565d-106">You can control in Azure AD who has access to Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="3565d-106">You can control in Azure AD who has access to Adobe Creative Cloud.</span></span>
- <span data-ttu-id="3565d-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3565d-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3565d-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3565d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3565d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3565d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3565d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3565d-110">Prerequisites</span></span>

<span data-ttu-id="3565d-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3565d-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="3565d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3565d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3565d-113">An Adobe Creative Cloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3565d-113">An Adobe Creative Cloud single sign-on enabled subscription</span></span>
- <span data-ttu-id="3565d-114">An Adobe Creative Cloud Enterprise version required</span><span class="sxs-lookup"><span data-stu-id="3565d-114">An Adobe Creative Cloud Enterprise version required</span></span>

> [!NOTE]
> <span data-ttu-id="3565d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3565d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3565d-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3565d-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3565d-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3565d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3565d-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3565d-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3565d-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3565d-119">Scenario description</span></span>

<span data-ttu-id="3565d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3565d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3565d-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3565d-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3565d-122">Adding Adobe Creative Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3565d-122">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="3565d-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3565d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="3565d-124">Adding Adobe Creative Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3565d-124">Adding Adobe Creative Cloud from the gallery</span></span>

<span data-ttu-id="3565d-125">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3565d-125">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3565d-126">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3565d-126">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3565d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3565d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="3565d-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3565d-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3565d-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3565d-130">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="3565d-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="3565d-134">In the search box, type **Adobe Creative Cloud**, select **Adobe Creative Cloud** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3565d-134">In the search box, type **Adobe Creative Cloud**, select **Adobe Creative Cloud** from result panel then click **Add** button to add the application.</span></span>

    ![Adobe Creative Cloud in the results list](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3565d-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3565d-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3565d-137">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3565d-137">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3565d-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3565d-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="3565d-139">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3565d-139">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="3565d-140">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3565d-140">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3565d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3565d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3565d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3565d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3565d-143">**[Create an Adobe Creative Cloud test user](#create-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3565d-143">**[Create an Adobe Creative Cloud test user](#create-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3565d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3565d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3565d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3565d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3565d-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3565d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3565d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Creative Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3565d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="3565d-148">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3565d-148">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3565d-149">In the Azure portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3565d-149">In the Azure portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="3565d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3565d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_samlbase.png)

3. <span data-ttu-id="3565d-153">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3565d-153">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Adobe Creative Cloud Domain and URLs single sign-on information](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_url.png)

    <span data-ttu-id="3565d-155">a.</span><span class="sxs-lookup"><span data-stu-id="3565d-155">a.</span></span> <span data-ttu-id="3565d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="3565d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="3565d-157">b.</span><span class="sxs-lookup"><span data-stu-id="3565d-157">b.</span></span> <span data-ttu-id="3565d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="3565d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3565d-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="3565d-159">These values are not real.</span></span> <span data-ttu-id="3565d-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="3565d-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="3565d-161">Contact [Adobe Creative Cloud Enterprise](https://www.adobe.com/au/creativecloud/business/teams/plans.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="3565d-161">Contact [Adobe Creative Cloud Enterprise](https://www.adobe.com/au/creativecloud/business/teams/plans.html) to get these values.</span></span>

4. <span data-ttu-id="3565d-162">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3565d-162">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Adobe Creative Cloud Domain and URLs single sign-on information](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_url2.png)

    <span data-ttu-id="3565d-164">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="3565d-164">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="3565d-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3565d-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_certificate.png)
     
6. <span data-ttu-id="3565d-167">Adobe Creative Cloud application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="3565d-167">Adobe Creative Cloud application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3565d-168">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="3565d-168">Configure the following claims for this application.</span></span> <span data-ttu-id="3565d-169">You can manage the values of these attributes from the **User Attribute** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="3565d-169">You can manage the values of these attributes from the **User Attribute** tab of the application.</span></span> <span data-ttu-id="3565d-170">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="3565d-170">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/adobe-creative-cloud-tutorial/tutorial_attribute.png)

7. <span data-ttu-id="3565d-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3565d-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="3565d-173">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="3565d-173">Attribute Name</span></span> | <span data-ttu-id="3565d-174">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="3565d-174">Attribute Value</span></span> |
    | ---------------| ----------------|
    | <span data-ttu-id="3565d-175">FirstName</span><span class="sxs-lookup"><span data-stu-id="3565d-175">FirstName</span></span> |<span data-ttu-id="3565d-176">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3565d-176">user.givenname</span></span> |
    | <span data-ttu-id="3565d-177">LastName</span><span class="sxs-lookup"><span data-stu-id="3565d-177">LastName</span></span> |<span data-ttu-id="3565d-178">user.surname</span><span class="sxs-lookup"><span data-stu-id="3565d-178">user.surname</span></span> |
    | <span data-ttu-id="3565d-179">Email</span><span class="sxs-lookup"><span data-stu-id="3565d-179">Email</span></span> |<span data-ttu-id="3565d-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="3565d-180">user.mail</span></span> |

    <span data-ttu-id="3565d-181">a.</span><span class="sxs-lookup"><span data-stu-id="3565d-181">a.</span></span> <span data-ttu-id="3565d-182">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/adobe-creative-cloud-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/adobe-creative-cloud-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3565d-185">b.</span><span class="sxs-lookup"><span data-stu-id="3565d-185">b.</span></span> <span data-ttu-id="3565d-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3565d-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3565d-187">c.</span><span class="sxs-lookup"><span data-stu-id="3565d-187">c.</span></span> <span data-ttu-id="3565d-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="3565d-188">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3565d-189">d.</span><span class="sxs-lookup"><span data-stu-id="3565d-189">d.</span></span> <span data-ttu-id="3565d-190">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="3565d-190">Click **Ok**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3565d-191">Users need to have a valid Office 365 ExO license for email claim value to be populated in the SAML response.</span><span class="sxs-lookup"><span data-stu-id="3565d-191">Users need to have a valid Office 365 ExO license for email claim value to be populated in the SAML response.</span></span>

8. <span data-ttu-id="3565d-192">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3565d-192">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/adobe-creative-cloud-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="3565d-194">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3565d-194">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3565d-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section**.</span><span class="sxs-lookup"><span data-stu-id="3565d-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Adobe Creative Cloud Configuration](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_configure.png)

10. <span data-ttu-id="3565d-197">In a different web browser window, sign-in to [Adobe Admin Console](https://adminconsole.adobe.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3565d-197">In a different web browser window, sign-in to [Adobe Admin Console](https://adminconsole.adobe.com) as an administrator.</span></span>

11. <span data-ttu-id="3565d-198">Go to **Settings** on the top navigation bar and then choose **Identity**.</span><span class="sxs-lookup"><span data-stu-id="3565d-198">Go to **Settings** on the top navigation bar and then choose **Identity**.</span></span> <span data-ttu-id="3565d-199">The list of domains opens.</span><span class="sxs-lookup"><span data-stu-id="3565d-199">The list of domains opens.</span></span> <span data-ttu-id="3565d-200">Click **Configure** link against your domain.</span><span class="sxs-lookup"><span data-stu-id="3565d-200">Click **Configure** link against your domain.</span></span> <span data-ttu-id="3565d-201">Then perform the following steps on **Single Sign On Configuration Required** section.</span><span class="sxs-lookup"><span data-stu-id="3565d-201">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span> <span data-ttu-id="3565d-202">For more information, see [Setup a domain](https://helpx.adobe.com/enterprise/using/set-up-domain.html)</span><span class="sxs-lookup"><span data-stu-id="3565d-202">For more information, see [Setup a domain](https://helpx.adobe.com/enterprise/using/set-up-domain.html)</span></span>

    <span data-ttu-id="3565d-203">![Settings](https://helpx.adobe.com/content/dam/help/en/enterprise/using/configure-microsoft-azure-with-adobe-sso/_jcr_content/main-pars/procedure_719391630/proc_par/step_3/step_par/image/edit-sso-configuration.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="3565d-203">![Settings](https://helpx.adobe.com/content/dam/help/en/enterprise/using/configure-microsoft-azure-with-adobe-sso/_jcr_content/main-pars/procedure_719391630/proc_par/step_3/step_par/image/edit-sso-configuration.png "Settings")</span></span>

    <span data-ttu-id="3565d-204">a.</span><span class="sxs-lookup"><span data-stu-id="3565d-204">a.</span></span> <span data-ttu-id="3565d-205">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span><span class="sxs-lookup"><span data-stu-id="3565d-205">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

    <span data-ttu-id="3565d-206">b.</span><span class="sxs-lookup"><span data-stu-id="3565d-206">b.</span></span> <span data-ttu-id="3565d-207">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3565d-207">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

    <span data-ttu-id="3565d-208">c.</span><span class="sxs-lookup"><span data-stu-id="3565d-208">c.</span></span> <span data-ttu-id="3565d-209">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3565d-209">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

    <span data-ttu-id="3565d-210">d.</span><span class="sxs-lookup"><span data-stu-id="3565d-210">d.</span></span> <span data-ttu-id="3565d-211">Select **HTTP - Redirect** as **IDP Binding**.</span><span class="sxs-lookup"><span data-stu-id="3565d-211">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

    <span data-ttu-id="3565d-212">e.</span><span class="sxs-lookup"><span data-stu-id="3565d-212">e.</span></span> <span data-ttu-id="3565d-213">Select **Email Address** as **User Login Setting**.</span><span class="sxs-lookup"><span data-stu-id="3565d-213">Select **Email Address** as **User Login Setting**.</span></span>

    <span data-ttu-id="3565d-214">f.</span><span class="sxs-lookup"><span data-stu-id="3565d-214">f.</span></span> <span data-ttu-id="3565d-215">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3565d-215">Click **Save** button.</span></span>

12. <span data-ttu-id="3565d-216">The dashboard will now present the XML **"Download Metadata"** file.</span><span class="sxs-lookup"><span data-stu-id="3565d-216">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="3565d-217">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span><span class="sxs-lookup"><span data-stu-id="3565d-217">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="3565d-218">Please open the file and configure them in the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="3565d-218">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configure Single Sign-On On App Side](./media/adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="3565d-220">a.</span><span class="sxs-lookup"><span data-stu-id="3565d-220">a.</span></span> <span data-ttu-id="3565d-221">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-221">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="3565d-222">b.</span><span class="sxs-lookup"><span data-stu-id="3565d-222">b.</span></span> <span data-ttu-id="3565d-223">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-223">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3565d-224">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3565d-224">Create an Azure AD test user</span></span>

<span data-ttu-id="3565d-225">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3565d-225">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3565d-227">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3565d-227">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3565d-228">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3565d-228">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/adobe-creative-cloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3565d-230">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3565d-230">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/adobe-creative-cloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3565d-232">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3565d-232">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/adobe-creative-cloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3565d-234">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3565d-234">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/adobe-creative-cloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3565d-236">a.</span><span class="sxs-lookup"><span data-stu-id="3565d-236">a.</span></span> <span data-ttu-id="3565d-237">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3565d-237">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3565d-238">b.</span><span class="sxs-lookup"><span data-stu-id="3565d-238">b.</span></span> <span data-ttu-id="3565d-239">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3565d-239">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3565d-240">c.</span><span class="sxs-lookup"><span data-stu-id="3565d-240">c.</span></span> <span data-ttu-id="3565d-241">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3565d-241">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3565d-242">d.</span><span class="sxs-lookup"><span data-stu-id="3565d-242">d.</span></span> <span data-ttu-id="3565d-243">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3565d-243">Click **Create**.</span></span>
 
### <a name="create-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="3565d-244">Create an Adobe Creative Cloud test user</span><span class="sxs-lookup"><span data-stu-id="3565d-244">Create an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="3565d-245">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="3565d-245">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span> <span data-ttu-id="3565d-246">In the case of Adobe Creative Cloud, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3565d-246">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="3565d-247">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3565d-247">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="3565d-248">Sign in to [Adobe Admin Console](https://adminconsole.adobe.com) site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3565d-248">Sign in to [Adobe Admin Console](https://adminconsole.adobe.com) site as an administrator.</span></span>

2. <span data-ttu-id="3565d-249">Add the user within Adobe’s console as Federated ID and assign them to a Product Profile.</span><span class="sxs-lookup"><span data-stu-id="3565d-249">Add the user within Adobe’s console as Federated ID and assign them to a Product Profile.</span></span> <span data-ttu-id="3565d-250">For detailed information on adding users, see [Add users in Adobe Admin Console](https://helpx.adobe.com/enterprise/using/users.html#Addusers)</span><span class="sxs-lookup"><span data-stu-id="3565d-250">For detailed information on adding users, see [Add users in Adobe Admin Console](https://helpx.adobe.com/enterprise/using/users.html#Addusers)</span></span> 

3. <span data-ttu-id="3565d-251">At this point, type your email address/upn into the Adobe signin form, press tab, and you should be federated back to Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3565d-251">At this point, type your email address/upn into the Adobe signin form, press tab, and you should be federated back to Azure AD:</span></span>
    * <span data-ttu-id="3565d-252">Web access: www.adobe.com > sign-in</span><span class="sxs-lookup"><span data-stu-id="3565d-252">Web access: www.adobe.com > sign-in</span></span>
    * <span data-ttu-id="3565d-253">Within the desktop app utility > sign-in</span><span class="sxs-lookup"><span data-stu-id="3565d-253">Within the desktop app utility > sign-in</span></span>
    * <span data-ttu-id="3565d-254">Within the application > help > sign-in</span><span class="sxs-lookup"><span data-stu-id="3565d-254">Within the application > help > sign-in</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3565d-255">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3565d-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="3565d-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="3565d-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Creative Cloud.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3565d-258">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3565d-258">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3565d-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3565d-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3565d-261">In the applications list, select **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3565d-261">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![The Adobe Creative Cloud link in the Applications list](./media/adobe-creative-cloud-tutorial/tutorial_adobecreativecloud_app.png)  

3. <span data-ttu-id="3565d-263">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3565d-263">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="3565d-265">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3565d-265">Click **Add** button.</span></span> <span data-ttu-id="3565d-266">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="3565d-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3565d-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3565d-269">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3565d-270">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3565d-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3565d-271">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3565d-271">Test single sign-on</span></span>

<span data-ttu-id="3565d-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3565d-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3565d-273">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3565d-273">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>
<span data-ttu-id="3565d-274">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3565d-274">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3565d-275">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3565d-275">Additional resources</span></span>

* [<span data-ttu-id="3565d-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3565d-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3565d-277">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3565d-277">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="3565d-278">Set up a domain (adobe.com)</span><span class="sxs-lookup"><span data-stu-id="3565d-278">Set up a domain (adobe.com)</span></span>](https://helpx.adobe.com/enterprise/using/set-up-domain.html)
* [<span data-ttu-id="3565d-279">Configure Azure for use with Adobe SSO (adobe.com)</span><span class="sxs-lookup"><span data-stu-id="3565d-279">Configure Azure for use with Adobe SSO (adobe.com)</span></span>](https://helpx.adobe.com/enterprise/kb/configure-microsoft-azure-with-adobe-sso.html)

<!--Image references-->

[1]: ./media/adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/adobe-creative-cloud-tutorial/tutorial_general_203.png
