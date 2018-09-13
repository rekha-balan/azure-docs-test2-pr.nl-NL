---
title: 'Tutorial: Azure Active Directory integration with ServiceNow | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ServiceNow.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a5a1a264-7497-47e7-b129-a1b5b1ebff5b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: 5d5c4d5e26fa21488dd637805a4c22bd3ed18a7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857435"
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="c87f7-103">Tutorial: Azure Active Directory integration with ServiceNow</span><span class="sxs-lookup"><span data-stu-id="c87f7-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>

<span data-ttu-id="c87f7-104">In this tutorial, you learn how to integrate ServiceNow with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c87f7-104">In this tutorial, you learn how to integrate ServiceNow with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c87f7-105">Integrating ServiceNow with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c87f7-105">Integrating ServiceNow with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c87f7-106">You can control in Azure AD who has access to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c87f7-106">You can control in Azure AD who has access to ServiceNow.</span></span>
- <span data-ttu-id="c87f7-107">You can enable your users to automatically get signed-on to ServiceNow (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c87f7-107">You can enable your users to automatically get signed-on to ServiceNow (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c87f7-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c87f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c87f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c87f7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c87f7-110">Prerequisites</span></span>

<span data-ttu-id="c87f7-111">To configure Azure AD integration with ServiceNow, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c87f7-111">To configure Azure AD integration with ServiceNow, you need the following items:</span></span>

- <span data-ttu-id="c87f7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c87f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c87f7-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span><span class="sxs-lookup"><span data-stu-id="c87f7-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
- <span data-ttu-id="c87f7-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span><span class="sxs-lookup"><span data-stu-id="c87f7-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
- <span data-ttu-id="c87f7-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span><span class="sxs-lookup"><span data-stu-id="c87f7-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="c87f7-116">This can be done by [submitting a service request](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="c87f7-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span>
- <span data-ttu-id="c87f7-117">For automatic configuration, enable the multi-provider plugin for ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c87f7-117">For automatic configuration, enable the multi-provider plugin for ServiceNow.</span></span>

> [!NOTE]
> <span data-ttu-id="c87f7-118">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c87f7-118">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c87f7-119">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c87f7-119">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c87f7-120">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c87f7-120">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c87f7-121">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c87f7-121">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c87f7-122">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c87f7-122">Scenario description</span></span>
<span data-ttu-id="c87f7-123">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c87f7-123">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c87f7-124">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c87f7-124">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c87f7-125">Adding ServiceNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="c87f7-125">Adding ServiceNow from the gallery</span></span>
1. <span data-ttu-id="c87f7-126">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c87f7-126">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="c87f7-127">Adding ServiceNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="c87f7-127">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="c87f7-128">To configure the integration of ServiceNow into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c87f7-128">To configure the integration of ServiceNow into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c87f7-129">**To add ServiceNow from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c87f7-129">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c87f7-130">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c87f7-130">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c87f7-132">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-132">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c87f7-133">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-133">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c87f7-135">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c87f7-135">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c87f7-137">In the search box, type **ServiceNow**, select **ServiceNow** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c87f7-137">In the search box, type **ServiceNow**, select **ServiceNow** from result panel then click **Add** button to add the application.</span></span>

    ![ServiceNow in the results list](./media/servicenow-tutorial/tutorial_servicenow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c87f7-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c87f7-139">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c87f7-140">In this section, you configure and test Azure AD single sign-on with ServiceNow based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c87f7-140">In this section, you configure and test Azure AD single sign-on with ServiceNow based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c87f7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c87f7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="c87f7-142">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c87f7-142">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>

<span data-ttu-id="c87f7-143">In ServiceNow, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c87f7-143">In ServiceNow, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c87f7-144">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c87f7-144">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c87f7-145">**[Configure Azure AD Single Sign-On for ServiceNow](#configure-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c87f7-145">**[Configure Azure AD Single Sign-On for ServiceNow](#configure-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c87f7-146">**[Configure Azure AD Single Sign-On for ServiceNow Express](#configure-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c87f7-146">**[Configure Azure AD Single Sign-On for ServiceNow Express](#configure-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c87f7-147">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c87f7-147">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c87f7-148">**[Create a ServiceNow test user](#create-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c87f7-148">**[Create a ServiceNow test user](#create-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c87f7-149">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c87f7-149">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c87f7-150">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c87f7-150">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="c87f7-151">Configure Azure AD Single Sign-On for ServiceNow</span><span class="sxs-lookup"><span data-stu-id="c87f7-151">Configure Azure AD Single Sign-On for ServiceNow</span></span>

<span data-ttu-id="c87f7-152">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ServiceNow application.</span><span class="sxs-lookup"><span data-stu-id="c87f7-152">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ServiceNow application.</span></span>

<span data-ttu-id="c87f7-153">**To configure Azure AD single sign-on with ServiceNow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c87f7-153">**To configure Azure AD single sign-on with ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="c87f7-154">In the Azure portal, on the **ServiceNow** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-154">In the Azure portal, on the **ServiceNow** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c87f7-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c87f7-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/servicenow-tutorial/tutorial_servicenow_samlbase.png)

1. <span data-ttu-id="c87f7-158">On the **ServiceNow Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-158">On the **ServiceNow Domain and URLs** section, perform the following steps:</span></span>

    ![ServiceNow Domain and URLs single sign-on information](./media/servicenow-tutorial/tutorial_servicenow_url.png)

    <span data-ttu-id="c87f7-160">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-160">a.</span></span> <span data-ttu-id="c87f7-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com/navpage.do`</span><span class="sxs-lookup"><span data-stu-id="c87f7-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com/navpage.do`</span></span>

    <span data-ttu-id="c87f7-162">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-162">b.</span></span> <span data-ttu-id="c87f7-163">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com`</span><span class="sxs-lookup"><span data-stu-id="c87f7-163">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c87f7-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="c87f7-164">These values are not real.</span></span> <span data-ttu-id="c87f7-165">You'll need to update these values from actual Sign-on URL and Identifier which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c87f7-165">You'll need to update these values from actual Sign-on URL and Identifier which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="c87f7-166">On the **SAML Signing Certificate** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-166">On the **SAML Signing Certificate** section, perform the following steps:</span></span> 

    ![The Certificate download link](./media/servicenow-tutorial/tutorial_servicenow_certificate.png)

    <span data-ttu-id="c87f7-168">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-168">a.</span></span> <span data-ttu-id="c87f7-169">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad, as this App Federation Metadata Url will be used later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c87f7-169">Click the copy button to copy **App Federation Metadata Url** and paste it into notepad, as this App Federation Metadata Url will be used later in the tutorial.</span></span>

    <span data-ttu-id="c87f7-170">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-170">b.</span></span> <span data-ttu-id="c87f7-171">Click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c87f7-171">Click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

1. <span data-ttu-id="c87f7-172">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c87f7-172">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/servicenow-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c87f7-174">Sign on to your ServiceNow application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c87f7-174">Sign on to your ServiceNow application as an administrator.</span></span>

1. <span data-ttu-id="c87f7-175">Activate the **Integration - Multiple Provider Single Sign-On Installer** plugin by following the next steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-175">Activate the **Integration - Multiple Provider Single Sign-On Installer** plugin by following the next steps:</span></span>

    <span data-ttu-id="c87f7-176">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-176">a.</span></span> <span data-ttu-id="c87f7-177">In the navigation pane on the left side, search **System Definition** section from the search bar and then click **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-177">In the navigation pane on the left side, search **System Definition** section from the search bar and then click **Plugins**.</span></span>

    <span data-ttu-id="c87f7-178">![Activate plugin](./media/servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span><span class="sxs-lookup"><span data-stu-id="c87f7-178">![Activate plugin](./media/servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>

     <span data-ttu-id="c87f7-179">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-179">b.</span></span> <span data-ttu-id="c87f7-180">Search for **Integration - Multiple Provider Single Sign-On Installer**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-180">Search for **Integration - Multiple Provider Single Sign-On Installer**.</span></span>

     <span data-ttu-id="c87f7-181">![Activate plugin](./media/servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span><span class="sxs-lookup"><span data-stu-id="c87f7-181">![Activate plugin](./media/servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>

    <span data-ttu-id="c87f7-182">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-182">c.</span></span> <span data-ttu-id="c87f7-183">Select the plugin.</span><span class="sxs-lookup"><span data-stu-id="c87f7-183">Select the plugin.</span></span> <span data-ttu-id="c87f7-184">Right click and select **Activate/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-184">Right click and select **Activate/Upgrade**.</span></span>

    <span data-ttu-id="c87f7-185">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-185">d.</span></span> <span data-ttu-id="c87f7-186">Click the **Activate** button.</span><span class="sxs-lookup"><span data-stu-id="c87f7-186">Click the **Activate** button.</span></span>

1. <span data-ttu-id="c87f7-187">There are two ways in which **ServiceNow** can be configured automatic and manual.</span><span class="sxs-lookup"><span data-stu-id="c87f7-187">There are two ways in which **ServiceNow** can be configured automatic and manual.</span></span>

1. <span data-ttu-id="c87f7-188">For configuring **ServiceNow** automatically follow the below steps</span><span class="sxs-lookup"><span data-stu-id="c87f7-188">For configuring **ServiceNow** automatically follow the below steps</span></span>

    <span data-ttu-id="c87f7-189">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-189">a.</span></span> <span data-ttu-id="c87f7-190">Return to the **ServiceNow** Single-Sign on page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-190">Return to the **ServiceNow** Single-Sign on page in the Azure portal.</span></span>

    <span data-ttu-id="c87f7-191">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-191">b.</span></span> <span data-ttu-id="c87f7-192">One click configure service is provided for ServiceNow that is, to have Azure AD automatically configure ServiceNow for SAML-based authentication.</span><span class="sxs-lookup"><span data-stu-id="c87f7-192">One click configure service is provided for ServiceNow that is, to have Azure AD automatically configure ServiceNow for SAML-based authentication.</span></span> <span data-ttu-id="c87f7-193">To enable this service go to **ServiceNow Configuration** section, click **Configure ServiceNow** to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="c87f7-193">To enable this service go to **ServiceNow Configuration** section, click **Configure ServiceNow** to open Configure sign-on window.</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_servicenow_configure.png)

    <span data-ttu-id="c87f7-195">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-195">c.</span></span> <span data-ttu-id="c87f7-196">Enter your ServiceNow instance name, admin username, and admin password in the **Configure sign-on** form and click **Configure Now**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-196">Enter your ServiceNow instance name, admin username, and admin password in the **Configure sign-on** form and click **Configure Now**.</span></span> <span data-ttu-id="c87f7-197">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span><span class="sxs-lookup"><span data-stu-id="c87f7-197">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="c87f7-198">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure single sign-on** and copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="c87f7-198">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure single sign-on** and copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the Quick Reference section.</span></span>

    <span data-ttu-id="c87f7-199">![Configure app URL](./media/servicenow-tutorial/configure.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-199">![Configure app URL](./media/servicenow-tutorial/configure.png "Configure app URL")</span></span>

    <span data-ttu-id="c87f7-200">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-200">d.</span></span> <span data-ttu-id="c87f7-201">Sign on to your ServiceNow application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c87f7-201">Sign on to your ServiceNow application as an administrator.</span></span>

    <span data-ttu-id="c87f7-202">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-202">e.</span></span> <span data-ttu-id="c87f7-203">In the automatic configuration all the necessary settings are configured on the **ServiceNow** side but the **X.509 Certificate** is not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="c87f7-203">In the automatic configuration all the necessary settings are configured on the **ServiceNow** side but the **X.509 Certificate** is not enabled by default.</span></span> <span data-ttu-id="c87f7-204">You have to map it manually to your identity provider in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c87f7-204">You have to map it manually to your identity provider in ServiceNow.</span></span> <span data-ttu-id="c87f7-205">follow the below steps for the same:</span><span class="sxs-lookup"><span data-stu-id="c87f7-205">follow the below steps for the same:</span></span>
    
    * <span data-ttu-id="c87f7-206">In the navigation pane on the left side, click **Identity Providers** Under **Multi-Provider SSO**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-206">In the navigation pane on the left side, click **Identity Providers** Under **Multi-Provider SSO**.</span></span>

      <span data-ttu-id="c87f7-207">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-207">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

    * <span data-ttu-id="c87f7-208">Click on the automatically generated identity provider</span><span class="sxs-lookup"><span data-stu-id="c87f7-208">Click on the automatically generated identity provider</span></span>

      <span data-ttu-id="c87f7-209">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_08.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-209">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_08.png "Configure single sign-on")</span></span>

    * <span data-ttu-id="c87f7-210">Scroll down to the **X.509 Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="c87f7-210">Scroll down to the **X.509 Certificate** section.</span></span> <span data-ttu-id="c87f7-211">Select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-211">Select **Edit**.</span></span>

      <span data-ttu-id="c87f7-212">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_09.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-212">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_09.png "Configure single sign-on")</span></span>
    
    * <span data-ttu-id="c87f7-213">Select on the certificate and click right arrow icon to add the certificate</span><span class="sxs-lookup"><span data-stu-id="c87f7-213">Select on the certificate and click right arrow icon to add the certificate</span></span>

      <span data-ttu-id="c87f7-214">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_11.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-214">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_11.png "Configure single sign-on")</span></span>

    * <span data-ttu-id="c87f7-215">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-215">Click **Save**.</span></span>

    * <span data-ttu-id="c87f7-216">Click on **Activate** at the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="c87f7-216">Click on **Activate** at the top right corner of the page.</span></span>

1. <span data-ttu-id="c87f7-217">For configuring **ServiceNow** manually follow the below steps</span><span class="sxs-lookup"><span data-stu-id="c87f7-217">For configuring **ServiceNow** manually follow the below steps</span></span>

1. <span data-ttu-id="c87f7-218">Sign on to your ServiceNow application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c87f7-218">Sign on to your ServiceNow application as an administrator.</span></span>

1. <span data-ttu-id="c87f7-219">In the navigation pane on the left side, search **Multi-Provider SSO** section from the search bar and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-219">In the navigation pane on the left side, search **Multi-Provider SSO** section from the search bar and then click **Properties**.</span></span>

    <span data-ttu-id="c87f7-220">![Configure app URL](./media/servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-220">![Configure app URL](./media/servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

1. <span data-ttu-id="c87f7-221">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-221">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-222">![Configure app URL](./media/servicenow-tutorial/ic7694981.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-222">![Configure app URL](./media/servicenow-tutorial/ic7694981.png "Configure app URL")</span></span>

    <span data-ttu-id="c87f7-223">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-223">a.</span></span> <span data-ttu-id="c87f7-224">As **Enable multiple provider SSO**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-224">As **Enable multiple provider SSO**, select **Yes**.</span></span>

    <span data-ttu-id="c87f7-225">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-225">b.</span></span> <span data-ttu-id="c87f7-226">As **Enable Auto Importing of users from all identity providers into the user table**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-226">As **Enable Auto Importing of users from all identity providers into the user table**, select **Yes**.</span></span>

    <span data-ttu-id="c87f7-227">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-227">c.</span></span> <span data-ttu-id="c87f7-228">As **Enable debug logging for the multiple provider SSO integration**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-228">As **Enable debug logging for the multiple provider SSO integration**, select **Yes**.</span></span>

    <span data-ttu-id="c87f7-229">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-229">d.</span></span> <span data-ttu-id="c87f7-230">In **The field on the user table that...** textbox, type **user_name**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-230">In **The field on the user table that...** textbox, type **user_name**.</span></span>

    <span data-ttu-id="c87f7-231">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-231">e.</span></span> <span data-ttu-id="c87f7-232">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-232">Click **Save**.</span></span>

1. <span data-ttu-id="c87f7-233">In the navigation pane on the left side, search **Multi-Provider SSO** section from the search bar and then click **x509 Certificates**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-233">In the navigation pane on the left side, search **Multi-Provider SSO** section from the search bar and then click **x509 Certificates**.</span></span>

    <span data-ttu-id="c87f7-234">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-234">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-235">On the **X.509 Certificates** dialog, click **New**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-235">On the **X.509 Certificates** dialog, click **New**.</span></span>

    <span data-ttu-id="c87f7-236">![Configure single sign-on](./media/servicenow-tutorial/ic7694974.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-236">![Configure single sign-on](./media/servicenow-tutorial/ic7694974.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-237">On the **X.509 Certificates** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-237">On the **X.509 Certificates** dialog, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-238">![Configure single sign-on](./media/servicenow-tutorial/ic7694975.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-238">![Configure single sign-on](./media/servicenow-tutorial/ic7694975.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-239">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-239">a.</span></span> <span data-ttu-id="c87f7-240">In the **Name** textbox, type a name for your configuration (for example: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="c87f7-240">In the **Name** textbox, type a name for your configuration (for example: **TestSAML2.0**).</span></span>

    <span data-ttu-id="c87f7-241">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-241">b.</span></span> <span data-ttu-id="c87f7-242">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-242">Select **Active**.</span></span>

    <span data-ttu-id="c87f7-243">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-243">c.</span></span> <span data-ttu-id="c87f7-244">As **Format**, select **PEM**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-244">As **Format**, select **PEM**.</span></span>

    <span data-ttu-id="c87f7-245">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-245">d.</span></span> <span data-ttu-id="c87f7-246">As **Type**, select **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-246">As **Type**, select **Trust Store Cert**.</span></span>

    <span data-ttu-id="c87f7-247">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-247">e.</span></span> <span data-ttu-id="c87f7-248">Open your Base64 encoded certificate downloaded from Azure in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="c87f7-248">Open your Base64 encoded certificate downloaded from Azure in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>

     <span data-ttu-id="c87f7-249">f.</span><span class="sxs-lookup"><span data-stu-id="c87f7-249">f.</span></span> <span data-ttu-id="c87f7-250">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-250">Click **Submit**.</span></span>

1. <span data-ttu-id="c87f7-251">In the navigation pane on the left side, click **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-251">In the navigation pane on the left side, click **Identity Providers**.</span></span>

    <span data-ttu-id="c87f7-252">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-252">![Configure single sign-on](./media/servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-253">On the **Identity Providers** dialog, click **New**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-253">On the **Identity Providers** dialog, click **New**.</span></span>

    <span data-ttu-id="c87f7-254">![Configure single sign-on](./media/servicenow-tutorial/ic7694977.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-254">![Configure single sign-on](./media/servicenow-tutorial/ic7694977.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-255">On the **Identity Providers** dialog, click **SAML2 Update1?**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-255">On the **Identity Providers** dialog, click **SAML2 Update1?**.</span></span>

    <span data-ttu-id="c87f7-256">![Configure single sign-on](./media/servicenow-tutorial/ic7694978.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-256">![Configure single sign-on](./media/servicenow-tutorial/ic7694978.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-257">On the SAML2 Update1 Properties dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-257">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-258">![Configure single sign-on](./media/servicenow-tutorial/idp.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-258">![Configure single sign-on](./media/servicenow-tutorial/idp.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-259">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-259">a.</span></span> <span data-ttu-id="c87f7-260">Select **URL** option in **Import Identity Provider Metadata** dialogue box.</span><span class="sxs-lookup"><span data-stu-id="c87f7-260">Select **URL** option in **Import Identity Provider Metadata** dialogue box.</span></span>

    <span data-ttu-id="c87f7-261">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-261">b.</span></span> <span data-ttu-id="c87f7-262">Enter the **App Federation Metadata Url** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-262">Enter the **App Federation Metadata Url** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c87f7-263">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-263">c.</span></span> <span data-ttu-id="c87f7-264">Click **Import**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-264">Click **Import**.</span></span>

1. <span data-ttu-id="c87f7-265">It reads the IdP metadata URL and populates all the fields information.</span><span class="sxs-lookup"><span data-stu-id="c87f7-265">It reads the IdP metadata URL and populates all the fields information.</span></span>

    <span data-ttu-id="c87f7-266">![Configure single sign-on](./media/servicenow-tutorial/ic7694982.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-266">![Configure single sign-on](./media/servicenow-tutorial/ic7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-267">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-267">a.</span></span> <span data-ttu-id="c87f7-268">In the **Name** textbox, type a name for your configuration (for example, **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="c87f7-268">In the **Name** textbox, type a name for your configuration (for example, **SAML 2.0**).</span></span>
    
    <span data-ttu-id="c87f7-269">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-269">b.</span></span> <span data-ttu-id="c87f7-270">Copy **ServiceNow Homepage** value, paste it in the **Sign-on URL** textbox in **ServiceNow Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-270">Copy **ServiceNow Homepage** value, paste it in the **Sign-on URL** textbox in **ServiceNow Domain and URLs** section on Azure portal.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-271">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (for example:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="c87f7-271">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (for example:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="c87f7-272">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-272">c.</span></span> <span data-ttu-id="c87f7-273">Copy **Entity ID / Issuer** value, paste it in **Identifier** textbox in **ServiceNow Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-273">Copy **Entity ID / Issuer** value, paste it in **Identifier** textbox in **ServiceNow Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="c87f7-274">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-274">d.</span></span> <span data-ttu-id="c87f7-275">Click **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-275">Click **Advanced**.</span></span> <span data-ttu-id="c87f7-276">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span><span class="sxs-lookup"><span data-stu-id="c87f7-276">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-277">You can configure Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure portal and mapping the desired field to the **nameidentifier** attribute.</span><span class="sxs-lookup"><span data-stu-id="c87f7-277">You can configure Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="c87f7-278">The value stored for the selected attribute in Azure AD (for example, user principal name) must match the value stored in ServiceNow for the entered field (for example, user_name)</span><span class="sxs-lookup"><span data-stu-id="c87f7-278">The value stored for the selected attribute in Azure AD (for example, user principal name) must match the value stored in ServiceNow for the entered field (for example, user_name)</span></span>

    <span data-ttu-id="c87f7-279">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-279">e.</span></span> <span data-ttu-id="c87f7-280">Under **x509 Certificate**, lists the certificate you have created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c87f7-280">Under **x509 Certificate**, lists the certificate you have created in the previous step.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-281">ServiceNow does not allow activation of the Idp without clicking on the test connection button, to override the same, please follow the below steps.</span><span class="sxs-lookup"><span data-stu-id="c87f7-281">ServiceNow does not allow activation of the Idp without clicking on the test connection button, to override the same, please follow the below steps.</span></span>

1. <span data-ttu-id="c87f7-282">Click on the menu icon from your new identity provider that you created as part of the configuration and from the list select **copy sys_id**</span><span class="sxs-lookup"><span data-stu-id="c87f7-282">Click on the menu icon from your new identity provider that you created as part of the configuration and from the list select **copy sys_id**</span></span>

    <span data-ttu-id="c87f7-283">![Configure single sign-on](./media/servicenow-tutorial/ic7694992.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-283">![Configure single sign-on](./media/servicenow-tutorial/ic7694992.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-284">In the upper left search box, search for **sys_properties.list** and press enter.</span><span class="sxs-lookup"><span data-stu-id="c87f7-284">In the upper left search box, search for **sys_properties.list** and press enter.</span></span>

    <span data-ttu-id="c87f7-285">![Configure single sign-on](./media/servicenow-tutorial/ic7694993.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-285">![Configure single sign-on](./media/servicenow-tutorial/ic7694993.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-286">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-286">Click **New**.</span></span>

    <span data-ttu-id="c87f7-287">![Configure single sign-on](./media/servicenow-tutorial/ic7694994.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-287">![Configure single sign-on](./media/servicenow-tutorial/ic7694994.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-288">In the **System Property** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-288">In the **System Property** section, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-289">![Configure single sign-on](./media/servicenow-tutorial/ic7694995.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-289">![Configure single sign-on](./media/servicenow-tutorial/ic7694995.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-290">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-290">a.</span></span> <span data-ttu-id="c87f7-291">Enter `glide.authenticate.sso.redirect.idp` value in the name textbox.</span><span class="sxs-lookup"><span data-stu-id="c87f7-291">Enter `glide.authenticate.sso.redirect.idp` value in the name textbox.</span></span>

    <span data-ttu-id="c87f7-292">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-292">b.</span></span> <span data-ttu-id="c87f7-293">In the **Value** textbox, paste the copy sys_id value which you have copied in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="c87f7-293">In the **Value** textbox, paste the copy sys_id value which you have copied in the preceding steps.</span></span>

    <span data-ttu-id="c87f7-294">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-294">c.</span></span> <span data-ttu-id="c87f7-295">Select **Private**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-295">Select **Private**.</span></span>

    <span data-ttu-id="c87f7-296">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-296">d.</span></span> <span data-ttu-id="c87f7-297">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-297">Click **Submit**.</span></span>

1. <span data-ttu-id="c87f7-298">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-298">Click **New**.</span></span>

    <span data-ttu-id="c87f7-299">![Configure single sign-on](./media/servicenow-tutorial/ic7694994.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-299">![Configure single sign-on](./media/servicenow-tutorial/ic7694994.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-300">In the **System Property** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-300">In the **System Property** section, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-301">![Configure single sign-on](./media/servicenow-tutorial/ic7694996.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-301">![Configure single sign-on](./media/servicenow-tutorial/ic7694996.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-302">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-302">a.</span></span> <span data-ttu-id="c87f7-303">Enter `glide.authenticate.multisso.test.connection.mandatory` value in the name textbox.</span><span class="sxs-lookup"><span data-stu-id="c87f7-303">Enter `glide.authenticate.multisso.test.connection.mandatory` value in the name textbox.</span></span>

    <span data-ttu-id="c87f7-304">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-304">b.</span></span> <span data-ttu-id="c87f7-305">In the **Value** textbox, enter **false**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-305">In the **Value** textbox, enter **false**.</span></span>

    <span data-ttu-id="c87f7-306">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-306">c.</span></span> <span data-ttu-id="c87f7-307">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-307">Click **Submit**.</span></span>

1. <span data-ttu-id="c87f7-308">After doing above step, now you will be able to activate your new identity provider and your SSO should work</span><span class="sxs-lookup"><span data-stu-id="c87f7-308">After doing above step, now you will be able to activate your new identity provider and your SSO should work</span></span>

> [!NOTE]
> <span data-ttu-id="c87f7-309">Also please note that, you have to test your new Idp configuration in a new incognito window</span><span class="sxs-lookup"><span data-stu-id="c87f7-309">Also please note that, you have to test your new Idp configuration in a new incognito window</span></span>

### <a name="configure-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="c87f7-310">Configure Azure AD Single Sign-On for ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="c87f7-310">Configure Azure AD Single Sign-On for ServiceNow Express</span></span>

1. <span data-ttu-id="c87f7-311">In the Azure portal, on the **ServiceNow** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-311">In the Azure portal, on the **ServiceNow** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="c87f7-313">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c87f7-313">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_servicenow_samlbase.png)

1. <span data-ttu-id="c87f7-315">On the **ServiceNow Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-315">On the **ServiceNow Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_servicenow_url.png)

    <span data-ttu-id="c87f7-317">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-317">a.</span></span> <span data-ttu-id="c87f7-318">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance-name>.service-now.com/navpage.do`</span><span class="sxs-lookup"><span data-stu-id="c87f7-318">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance-name>.service-now.com/navpage.do`</span></span>

    <span data-ttu-id="c87f7-319">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-319">b.</span></span> <span data-ttu-id="c87f7-320">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com`</span><span class="sxs-lookup"><span data-stu-id="c87f7-320">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance-name>.service-now.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-321">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="c87f7-321">These values are not real.</span></span> <span data-ttu-id="c87f7-322">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="c87f7-322">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="c87f7-323">Contact [ServiceNow Client support team](https://www.servicenow.com/support/contact-support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="c87f7-323">Contact [ServiceNow Client support team](https://www.servicenow.com/support/contact-support.html) to get these values.</span></span>

1. <span data-ttu-id="c87f7-324">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c87f7-324">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_servicenow_certificates.png)

1. <span data-ttu-id="c87f7-326">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c87f7-326">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c87f7-328">One click configure service is provided for ServiceNow that is, to have Azure AD automatically configure ServiceNow for SAML-based authentication.</span><span class="sxs-lookup"><span data-stu-id="c87f7-328">One click configure service is provided for ServiceNow that is, to have Azure AD automatically configure ServiceNow for SAML-based authentication.</span></span> <span data-ttu-id="c87f7-329">To enable this service go to **ServiceNow Configuration** section, click **Configure ServiceNow** to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="c87f7-329">To enable this service go to **ServiceNow Configuration** section, click **Configure ServiceNow** to open Configure sign-on window.</span></span>

    ![Configure Single Sign-On](./media/servicenow-tutorial/tutorial_servicenow_configure.png)

1. <span data-ttu-id="c87f7-331">Enter your ServiceNow instance name, admin username, and admin password in the **Configure sign-on** form and click **Configure Now**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-331">Enter your ServiceNow instance name, admin username, and admin password in the **Configure sign-on** form and click **Configure Now**.</span></span> <span data-ttu-id="c87f7-332">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span><span class="sxs-lookup"><span data-stu-id="c87f7-332">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="c87f7-333">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure single sign-on** and copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="c87f7-333">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure single sign-on** and copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the Quick Reference section.</span></span>

    <span data-ttu-id="c87f7-334">![Configure app URL](./media/servicenow-tutorial/configure.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-334">![Configure app URL](./media/servicenow-tutorial/configure.png "Configure app URL")</span></span>

1. <span data-ttu-id="c87f7-335">Sign on to your ServiceNow Express application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c87f7-335">Sign on to your ServiceNow Express application as an administrator.</span></span>

1. <span data-ttu-id="c87f7-336">In the navigation pane on the left side, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-336">In the navigation pane on the left side, click **Single Sign-On**.</span></span>

    <span data-ttu-id="c87f7-337">![Configure app URL](./media/servicenow-tutorial/ic7694980ex.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-337">![Configure app URL](./media/servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

1. <span data-ttu-id="c87f7-338">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span><span class="sxs-lookup"><span data-stu-id="c87f7-338">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>

    <span data-ttu-id="c87f7-339">![Configure app URL](./media/servicenow-tutorial/ic7694981ex.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c87f7-339">![Configure app URL](./media/servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>

    <span data-ttu-id="c87f7-340">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-340">a.</span></span> <span data-ttu-id="c87f7-341">Toggle **Enable multiple provider SSO** to the right.</span><span class="sxs-lookup"><span data-stu-id="c87f7-341">Toggle **Enable multiple provider SSO** to the right.</span></span>
    
    <span data-ttu-id="c87f7-342">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-342">b.</span></span> <span data-ttu-id="c87f7-343">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span><span class="sxs-lookup"><span data-stu-id="c87f7-343">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
    
    <span data-ttu-id="c87f7-344">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-344">c.</span></span> <span data-ttu-id="c87f7-345">In **The field on the user table that...** textbox, type **user_name**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-345">In **The field on the user table that...** textbox, type **user_name**.</span></span>

1. <span data-ttu-id="c87f7-346">On the **Single Sign-On** dialog, click **Add New Certificate**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-346">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>

    <span data-ttu-id="c87f7-347">![Configure single sign-on](./media/servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-347">![Configure single sign-on](./media/servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-348">On the **X.509 Certificates** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-348">On the **X.509 Certificates** dialog, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-349">![Configure single sign-on](./media/servicenow-tutorial/ic7694975.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-349">![Configure single sign-on](./media/servicenow-tutorial/ic7694975.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-350">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-350">a.</span></span> <span data-ttu-id="c87f7-351">In the **Name** textbox, type a name for your configuration (for example: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="c87f7-351">In the **Name** textbox, type a name for your configuration (for example: **TestSAML2.0**).</span></span>

    <span data-ttu-id="c87f7-352">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-352">b.</span></span> <span data-ttu-id="c87f7-353">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-353">Select **Active**.</span></span>

    <span data-ttu-id="c87f7-354">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-354">c.</span></span> <span data-ttu-id="c87f7-355">As **Format**, select **PEM**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-355">As **Format**, select **PEM**.</span></span>

    <span data-ttu-id="c87f7-356">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-356">d.</span></span> <span data-ttu-id="c87f7-357">As **Type**, select **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-357">As **Type**, select **Trust Store Cert**.</span></span>

    <span data-ttu-id="c87f7-358">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-358">e.</span></span> <span data-ttu-id="c87f7-359">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="c87f7-359">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>

    <span data-ttu-id="c87f7-360">f.</span><span class="sxs-lookup"><span data-stu-id="c87f7-360">f.</span></span> <span data-ttu-id="c87f7-361">Click **Update**</span><span class="sxs-lookup"><span data-stu-id="c87f7-361">Click **Update**</span></span>

1. <span data-ttu-id="c87f7-362">On the **Single Sign-On** dialog, click **Add New IdP**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-362">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>

    <span data-ttu-id="c87f7-363">![Configure single sign-on](./media/servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-363">![Configure single sign-on](./media/servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>

1. <span data-ttu-id="c87f7-364">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-364">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-365">![Configure single sign-on](./media/servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-365">![Configure single sign-on](./media/servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-366">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-366">a.</span></span> <span data-ttu-id="c87f7-367">In the **Name** textbox, type a name for your configuration (for example: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="c87f7-367">In the **Name** textbox, type a name for your configuration (for example: **SAML 2.0**).</span></span>

    <span data-ttu-id="c87f7-368">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-368">b.</span></span> <span data-ttu-id="c87f7-369">In the **Identity Provider URL** field, paste the value of **Identity Provider ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-369">In the **Identity Provider URL** field, paste the value of **Identity Provider ID**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c87f7-370">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-370">c.</span></span> <span data-ttu-id="c87f7-371">In the **Identity Provider's AuthnRequest** field, paste the value of **Authentication Request URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c87f7-371">In the **Identity Provider's AuthnRequest** field, paste the value of **Authentication Request URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c87f7-372">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-372">d.</span></span> <span data-ttu-id="c87f7-373">In the **Identity Provider's SingleLogoutRequest** field, paste the value of **Single Sign-Out Service URL**, which you have copied from Azure portal</span><span class="sxs-lookup"><span data-stu-id="c87f7-373">In the **Identity Provider's SingleLogoutRequest** field, paste the value of **Single Sign-Out Service URL**, which you have copied from Azure portal</span></span>

    <span data-ttu-id="c87f7-374">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-374">e.</span></span> <span data-ttu-id="c87f7-375">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c87f7-375">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>

1. <span data-ttu-id="c87f7-376">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-376">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-377">![Configure single sign-on](./media/servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-377">![Configure single sign-on](./media/servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-378">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-378">a.</span></span> <span data-ttu-id="c87f7-379">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-379">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="c87f7-380">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-380">b.</span></span> <span data-ttu-id="c87f7-381">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-381">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="c87f7-382">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-382">c.</span></span> <span data-ttu-id="c87f7-383">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="c87f7-383">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span>

    <span data-ttu-id="c87f7-384">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-384">d.</span></span> <span data-ttu-id="c87f7-385">Deselect **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-385">Deselect **Create an AuthnContextClass**.</span></span>

1. <span data-ttu-id="c87f7-386">Under **Additional Service Provider Properties**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-386">Under **Additional Service Provider Properties**, perform the following steps:</span></span>

    <span data-ttu-id="c87f7-387">![Configure single sign-on](./media/servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c87f7-387">![Configure single sign-on](./media/servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="c87f7-388">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-388">a.</span></span> <span data-ttu-id="c87f7-389">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span><span class="sxs-lookup"><span data-stu-id="c87f7-389">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-390">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (for example: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="c87f7-390">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (for example: `https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="c87f7-391">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-391">b.</span></span> <span data-ttu-id="c87f7-392">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="c87f7-392">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="c87f7-393">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-393">c.</span></span> <span data-ttu-id="c87f7-394">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="c87f7-394">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="c87f7-395">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-395">d.</span></span> <span data-ttu-id="c87f7-396">In **Clock Skew** textbox, type **60**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-396">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="c87f7-397">e.</span><span class="sxs-lookup"><span data-stu-id="c87f7-397">e.</span></span> <span data-ttu-id="c87f7-398">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span><span class="sxs-lookup"><span data-stu-id="c87f7-398">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c87f7-399">You can configure Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure portal and mapping the desired field to the **nameidentifier** attribute.</span><span class="sxs-lookup"><span data-stu-id="c87f7-399">You can configure Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="c87f7-400">The value stored for the selected attribute in Azure AD (for example, user principal name) must match the value stored in ServiceNow for the entered field (for example, user_name)</span><span class="sxs-lookup"><span data-stu-id="c87f7-400">The value stored for the selected attribute in Azure AD (for example, user principal name) must match the value stored in ServiceNow for the entered field (for example, user_name)</span></span>

    <span data-ttu-id="c87f7-401">f.</span><span class="sxs-lookup"><span data-stu-id="c87f7-401">f.</span></span> <span data-ttu-id="c87f7-402">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-402">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c87f7-403">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c87f7-403">Create an Azure AD test user</span></span>

<span data-ttu-id="c87f7-404">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c87f7-404">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c87f7-406">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c87f7-406">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c87f7-407">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c87f7-407">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/servicenow-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c87f7-409">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-409">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/servicenow-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c87f7-411">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c87f7-411">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/servicenow-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c87f7-413">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c87f7-413">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/servicenow-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c87f7-415">a.</span><span class="sxs-lookup"><span data-stu-id="c87f7-415">a.</span></span> <span data-ttu-id="c87f7-416">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-416">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c87f7-417">b.</span><span class="sxs-lookup"><span data-stu-id="c87f7-417">b.</span></span> <span data-ttu-id="c87f7-418">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c87f7-418">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c87f7-419">c.</span><span class="sxs-lookup"><span data-stu-id="c87f7-419">c.</span></span> <span data-ttu-id="c87f7-420">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c87f7-420">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c87f7-421">d.</span><span class="sxs-lookup"><span data-stu-id="c87f7-421">d.</span></span> <span data-ttu-id="c87f7-422">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-422">Click **Create**.</span></span>

### <a name="create-a-servicenow-test-user"></a><span data-ttu-id="c87f7-423">Create a ServiceNow test user</span><span class="sxs-lookup"><span data-stu-id="c87f7-423">Create a ServiceNow test user</span></span>

<span data-ttu-id="c87f7-424">The objective of this section is to create a user called Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c87f7-424">The objective of this section is to create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="c87f7-425">ServiceNow supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="c87f7-425">ServiceNow supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="c87f7-426">You can find more details [here](servicenow-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="c87f7-426">You can find more details [here](servicenow-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="c87f7-427">If you need to create a user manually, you need to contact [ServiceNow Client support team](https://www.servicenow.com/support/contact-support.html)</span><span class="sxs-lookup"><span data-stu-id="c87f7-427">If you need to create a user manually, you need to contact [ServiceNow Client support team](https://www.servicenow.com/support/contact-support.html)</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c87f7-428">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c87f7-428">Assign the Azure AD test user</span></span>

<span data-ttu-id="c87f7-429">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="c87f7-429">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ServiceNow.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c87f7-431">**To assign Britta Simon to ServiceNow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c87f7-431">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="c87f7-432">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-432">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c87f7-434">In the applications list, select **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-434">In the applications list, select **ServiceNow**.</span></span>

    ![The ServiceNow link in the Applications list](./media/servicenow-tutorial/tutorial_servicenow_app.png)  

1. <span data-ttu-id="c87f7-436">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c87f7-436">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c87f7-438">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c87f7-438">Click **Add** button.</span></span> <span data-ttu-id="c87f7-439">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c87f7-439">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c87f7-441">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c87f7-441">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c87f7-442">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c87f7-442">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c87f7-443">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c87f7-443">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c87f7-444">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c87f7-444">Test single sign-on</span></span>

<span data-ttu-id="c87f7-445">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c87f7-445">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c87f7-446">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span><span class="sxs-lookup"><span data-stu-id="c87f7-446">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>
<span data-ttu-id="c87f7-447">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c87f7-447">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c87f7-448">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c87f7-448">Additional resources</span></span>

* [<span data-ttu-id="c87f7-449">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c87f7-449">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c87f7-450">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c87f7-450">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="c87f7-451">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="c87f7-451">Configure User Provisioning</span></span>](servicenow-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/servicenow-tutorial/tutorial_general_01.png
[2]: ./media/servicenow-tutorial/tutorial_general_02.png
[3]: ./media/servicenow-tutorial/tutorial_general_03.png
[4]: ./media/servicenow-tutorial/tutorial_general_04.png

[100]: ./media/servicenow-tutorial/tutorial_general_100.png

[200]: ./media/servicenow-tutorial/tutorial_general_200.png
[201]: ./media/servicenow-tutorial/tutorial_general_201.png
[202]: ./media/servicenow-tutorial/tutorial_general_202.png
[203]: ./media/servicenow-tutorial/tutorial_general_203.png
