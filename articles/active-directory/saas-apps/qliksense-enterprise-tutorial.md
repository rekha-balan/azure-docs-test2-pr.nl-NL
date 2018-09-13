---
title: 'Tutorial: Azure Active Directory integration with Qlik Sense Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Qlik Sense Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/06/2018
ms.author: jeedes
ms.openlocfilehash: a8816451b45171e0ba8cbd7acc937201c587c481
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858079"
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="5fee8-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="5fee8-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="5fee8-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fee8-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fee8-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5fee8-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5fee8-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5fee8-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="5fee8-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="5fee8-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5fee8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5fee8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5fee8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5fee8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fee8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5fee8-110">Prerequisites</span></span>

<span data-ttu-id="5fee8-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5fee8-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="5fee8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5fee8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fee8-113">A Qlik Sense Enterprise single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5fee8-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fee8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5fee8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fee8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5fee8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fee8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5fee8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fee8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fee8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fee8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5fee8-118">Scenario description</span></span>
<span data-ttu-id="5fee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5fee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fee8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5fee8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fee8-121">Adding Qlik Sense Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="5fee8-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="5fee8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5fee8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="5fee8-123">Adding Qlik Sense Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="5fee8-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="5fee8-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5fee8-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5fee8-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5fee8-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5fee8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5fee8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="5fee8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5fee8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="5fee8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5fee8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="5fee8-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5fee8-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise in the results list](./media/qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5fee8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5fee8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5fee8-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5fee8-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fee8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fee8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="5fee8-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5fee8-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="5fee8-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="5fee8-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5fee8-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5fee8-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5fee8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5fee8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5fee8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fee8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fee8-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5fee8-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fee8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5fee8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fee8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5fee8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5fee8-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5fee8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5fee8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="5fee8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="5fee8-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5fee8-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5fee8-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="5fee8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5fee8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="5fee8-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5fee8-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Qlik Sense Enterprise Domain and URLs single sign-on information](./media/qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="5fee8-155">a.</span><span class="sxs-lookup"><span data-stu-id="5fee8-155">a.</span></span> <span data-ttu-id="5fee8-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:4443/azure/hub`</span><span class="sxs-lookup"><span data-stu-id="5fee8-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:4443/azure/hub`</span></span>

    <span data-ttu-id="5fee8-157">b.</span><span class="sxs-lookup"><span data-stu-id="5fee8-157">b.</span></span> <span data-ttu-id="5fee8-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="5fee8-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|
    | |

    <span data-ttu-id="5fee8-159">c.</span><span class="sxs-lookup"><span data-stu-id="5fee8-159">c.</span></span> <span data-ttu-id="5fee8-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="5fee8-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    `https://<Qlik Sense Fully Qualifed Hostname>:4443/samlauthn/`

    > [!NOTE]
    > <span data-ttu-id="5fee8-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="5fee8-161">These values are not real.</span></span> <span data-ttu-id="5fee8-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="5fee8-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span>

4. <span data-ttu-id="5fee8-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5fee8-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png)

5. <span data-ttu-id="5fee8-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fee8-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5fee8-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>

    ![QlikSense][qs24]

    <span data-ttu-id="5fee8-170">a.</span><span class="sxs-lookup"><span data-stu-id="5fee8-170">a.</span></span> <span data-ttu-id="5fee8-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span><span class="sxs-lookup"><span data-stu-id="5fee8-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>

    <span data-ttu-id="5fee8-172">b.</span><span class="sxs-lookup"><span data-stu-id="5fee8-172">b.</span></span> <span data-ttu-id="5fee8-173">Search for the value **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="5fee8-174">There are four entries (two pairs of opening and closing element tags).</span><span class="sxs-lookup"><span data-stu-id="5fee8-174">There are four entries (two pairs of opening and closing element tags).</span></span>

    <span data-ttu-id="5fee8-175">c.</span><span class="sxs-lookup"><span data-stu-id="5fee8-175">c.</span></span> <span data-ttu-id="5fee8-176">Delete the RoleDescriptor tags and all information in between from the file.</span><span class="sxs-lookup"><span data-stu-id="5fee8-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>

    <span data-ttu-id="5fee8-177">d.</span><span class="sxs-lookup"><span data-stu-id="5fee8-177">d.</span></span> <span data-ttu-id="5fee8-178">Save the file and keep it nearby for use later in this document.</span><span class="sxs-lookup"><span data-stu-id="5fee8-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="5fee8-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span><span class="sxs-lookup"><span data-stu-id="5fee8-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="5fee8-180">In the QMC, click on the **Virtual Proxies** menu item.</span><span class="sxs-lookup"><span data-stu-id="5fee8-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>

    ![QlikSense][qs6]

9. <span data-ttu-id="5fee8-182">At the bottom of the screen, click the **Create new** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-182">At the bottom of the screen, click the **Create new** button.</span></span>

    ![QlikSense][qs7]

10. <span data-ttu-id="5fee8-184">The Virtual proxy edit screen appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="5fee8-185">On the right side of the screen is a menu for making configuration options visible.</span><span class="sxs-lookup"><span data-stu-id="5fee8-185">On the right side of the screen is a menu for making configuration options visible.</span></span>

    ![QlikSense][qs9]

11. <span data-ttu-id="5fee8-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>

    ![QlikSense][qs8]  

    <span data-ttu-id="5fee8-189">a.</span><span class="sxs-lookup"><span data-stu-id="5fee8-189">a.</span></span> <span data-ttu-id="5fee8-190">The **Description** field is a friendly name for the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="5fee8-191">Enter a value for a description.</span><span class="sxs-lookup"><span data-stu-id="5fee8-191">Enter a value for a description.</span></span>

    <span data-ttu-id="5fee8-192">b.</span><span class="sxs-lookup"><span data-stu-id="5fee8-192">b.</span></span> <span data-ttu-id="5fee8-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5fee8-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="5fee8-194">Enter a unique prefix name for this virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="5fee8-194">Enter a unique prefix name for this virtual proxy.</span></span>

    <span data-ttu-id="5fee8-195">c.</span><span class="sxs-lookup"><span data-stu-id="5fee8-195">c.</span></span> <span data-ttu-id="5fee8-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="5fee8-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>

    <span data-ttu-id="5fee8-197">d.</span><span class="sxs-lookup"><span data-stu-id="5fee8-197">d.</span></span> <span data-ttu-id="5fee8-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="5fee8-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="5fee8-199">This name must be unique.</span><span class="sxs-lookup"><span data-stu-id="5fee8-199">This name must be unique.</span></span>

12. <span data-ttu-id="5fee8-200">Click on the Authentication menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="5fee8-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="5fee8-201">The Authentication screen appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-201">The Authentication screen appears.</span></span>

    ![QlikSense][qs10]

    <span data-ttu-id="5fee8-203">a.</span><span class="sxs-lookup"><span data-stu-id="5fee8-203">a.</span></span> <span data-ttu-id="5fee8-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="5fee8-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="5fee8-205">The default option is No anonymous user.</span><span class="sxs-lookup"><span data-stu-id="5fee8-205">The default option is No anonymous user.</span></span>

    <span data-ttu-id="5fee8-206">b.</span><span class="sxs-lookup"><span data-stu-id="5fee8-206">b.</span></span> <span data-ttu-id="5fee8-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span><span class="sxs-lookup"><span data-stu-id="5fee8-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="5fee8-208">Select SAML from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="5fee8-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="5fee8-209">More options appear as a result.</span><span class="sxs-lookup"><span data-stu-id="5fee8-209">More options appear as a result.</span></span>

    <span data-ttu-id="5fee8-210">c.</span><span class="sxs-lookup"><span data-stu-id="5fee8-210">c.</span></span> <span data-ttu-id="5fee8-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="5fee8-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="5fee8-212">The hostname is the uri of the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-212">The hostname is the uri of the Qlik Sense server.</span></span>

    <span data-ttu-id="5fee8-213">d.</span><span class="sxs-lookup"><span data-stu-id="5fee8-213">d.</span></span> <span data-ttu-id="5fee8-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span><span class="sxs-lookup"><span data-stu-id="5fee8-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>

    <span data-ttu-id="5fee8-215">e.</span><span class="sxs-lookup"><span data-stu-id="5fee8-215">e.</span></span> <span data-ttu-id="5fee8-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="5fee8-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="5fee8-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="5fee8-218">**Please refer to the instructions above if the file has yet to be edited.**</span><span class="sxs-lookup"><span data-stu-id="5fee8-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="5fee8-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>

    <span data-ttu-id="5fee8-220">f.</span><span class="sxs-lookup"><span data-stu-id="5fee8-220">f.</span></span> <span data-ttu-id="5fee8-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="5fee8-222">Schema reference information is available in the Azure app screens post configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="5fee8-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5fee8-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="5fee8-224">g.</span><span class="sxs-lookup"><span data-stu-id="5fee8-224">g.</span></span> <span data-ttu-id="5fee8-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fee8-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="5fee8-226">Hardcoded values must be surrounded by **square brackets []**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="5fee8-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span><span class="sxs-lookup"><span data-stu-id="5fee8-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>

    <span data-ttu-id="5fee8-228">h.</span><span class="sxs-lookup"><span data-stu-id="5fee8-228">h.</span></span> <span data-ttu-id="5fee8-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="5fee8-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>

    <span data-ttu-id="5fee8-231">i.</span><span class="sxs-lookup"><span data-stu-id="5fee8-231">i.</span></span> <span data-ttu-id="5fee8-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span><span class="sxs-lookup"><span data-stu-id="5fee8-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="5fee8-233">Click on the **LOAD BALANCING** menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="5fee8-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="5fee8-234">The Load Balancing screen appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-234">The Load Balancing screen appears.</span></span>

    ![QlikSense][qs11]

14. <span data-ttu-id="5fee8-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>

    ![QlikSense][qs12]

15. <span data-ttu-id="5fee8-238">Click on the Advanced menu option to make it visible.</span><span class="sxs-lookup"><span data-stu-id="5fee8-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="5fee8-239">The Advanced screen appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-239">The Advanced screen appears.</span></span>

    ![QlikSense][qs13]

    <span data-ttu-id="5fee8-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span><span class="sxs-lookup"><span data-stu-id="5fee8-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="5fee8-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span><span class="sxs-lookup"><span data-stu-id="5fee8-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="5fee8-243">The hostname is the same value as the SAML host uri without the https://.</span><span class="sxs-lookup"><span data-stu-id="5fee8-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="5fee8-244">Click the **Apply** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-244">Click the **Apply** button.</span></span>

    ![QlikSense][qs14]

17. <span data-ttu-id="5fee8-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span><span class="sxs-lookup"><span data-stu-id="5fee8-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>

    ![QlikSense][qs15]

18. <span data-ttu-id="5fee8-248">On the right side of the screen, the Associated items menu appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="5fee8-249">Click on the **Proxies** menu option.</span><span class="sxs-lookup"><span data-stu-id="5fee8-249">Click on the **Proxies** menu option.</span></span>

    ![QlikSense][qs16]

19. <span data-ttu-id="5fee8-251">The proxy screen appears.</span><span class="sxs-lookup"><span data-stu-id="5fee8-251">The proxy screen appears.</span></span>  <span data-ttu-id="5fee8-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="5fee8-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>

    ![QlikSense][qs17]

20. <span data-ttu-id="5fee8-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="5fee8-255">After linking, the proxy will be listed under associated proxies.</span><span class="sxs-lookup"><span data-stu-id="5fee8-255">After linking, the proxy will be listed under associated proxies.</span></span>

    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="5fee8-258">After about five to ten seconds, the Refresh QMC message will appear.</span><span class="sxs-lookup"><span data-stu-id="5fee8-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="5fee8-259">Click the **Refresh QMC** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-259">Click the **Refresh QMC** button.</span></span>

    ![QlikSense][qs20]

22. <span data-ttu-id="5fee8-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span><span class="sxs-lookup"><span data-stu-id="5fee8-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="5fee8-262">The new SAML virtual proxy entry is listed in the table on the screen.</span><span class="sxs-lookup"><span data-stu-id="5fee8-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="5fee8-263">Single click on the virtual proxy entry.</span><span class="sxs-lookup"><span data-stu-id="5fee8-263">Single click on the virtual proxy entry.</span></span>

    ![QlikSense][qs51]

23. <span data-ttu-id="5fee8-265">At the bottom of the screen, the Download SP metadata button will activate.</span><span class="sxs-lookup"><span data-stu-id="5fee8-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="5fee8-266">Click the **Download SP metadata** button to save the metadata to a file.</span><span class="sxs-lookup"><span data-stu-id="5fee8-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>

    ![QlikSense][qs52]

24. <span data-ttu-id="5fee8-268">Open the sp metadata file.</span><span class="sxs-lookup"><span data-stu-id="5fee8-268">Open the sp metadata file.</span></span>  <span data-ttu-id="5fee8-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span><span class="sxs-lookup"><span data-stu-id="5fee8-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="5fee8-270">These values are equivalent to the **Identifier**, **Sign on URL** and the **Reply URL** in the Azure AD application configuration.</span><span class="sxs-lookup"><span data-stu-id="5fee8-270">These values are equivalent to the **Identifier**, **Sign on URL** and the **Reply URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="5fee8-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="5fee8-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>

    ![QlikSense][qs53]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5fee8-273">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5fee8-273">Create an Azure AD test user</span></span>

<span data-ttu-id="5fee8-274">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fee8-274">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="5fee8-276">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5fee8-276">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5fee8-277">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-277">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![The Azure Active Directory button](./media/qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5fee8-279">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-279">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![The "Users and groups" and "All users" links](./media/qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5fee8-281">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5fee8-281">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![The Add button](./media/qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5fee8-283">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5fee8-283">In the **User** dialog box, perform the following steps:</span></span>

   ![The User dialog box](./media/qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="5fee8-285">a.</span><span class="sxs-lookup"><span data-stu-id="5fee8-285">a.</span></span> <span data-ttu-id="5fee8-286">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-286">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="5fee8-287">b.</span><span class="sxs-lookup"><span data-stu-id="5fee8-287">b.</span></span> <span data-ttu-id="5fee8-288">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fee8-288">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="5fee8-289">c.</span><span class="sxs-lookup"><span data-stu-id="5fee8-289">c.</span></span> <span data-ttu-id="5fee8-290">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="5fee8-290">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="5fee8-291">d.</span><span class="sxs-lookup"><span data-stu-id="5fee8-291">d.</span></span> <span data-ttu-id="5fee8-292">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-292">Click **Create**.</span></span>

### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="5fee8-293">Create a Qlik Sense Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="5fee8-293">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="5fee8-294">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5fee8-294">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="5fee8-295">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span><span class="sxs-lookup"><span data-stu-id="5fee8-295">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="5fee8-296">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5fee8-296">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5fee8-297">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5fee8-297">Assign the Azure AD test user</span></span>

<span data-ttu-id="5fee8-298">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5fee8-298">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Assign the user role][200]

<span data-ttu-id="5fee8-300">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5fee8-300">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5fee8-301">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-301">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="5fee8-303">In the applications list, select **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-303">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![The Qlik Sense Enterprise link in the Applications list](./media/qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="5fee8-305">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5fee8-305">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="5fee8-307">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5fee8-307">Click **Add** button.</span></span> <span data-ttu-id="5fee8-308">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5fee8-308">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="5fee8-310">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5fee8-310">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5fee8-311">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5fee8-311">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fee8-312">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5fee8-312">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="5fee8-313">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5fee8-313">Test single sign-on</span></span>

<span data-ttu-id="5fee8-314">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5fee8-314">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5fee8-315">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="5fee8-315">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fee8-316">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5fee8-316">Additional resources</span></span>

* [<span data-ttu-id="5fee8-317">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fee8-317">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5fee8-318">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fee8-318">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png