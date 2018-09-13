---
title: 'Tutorial: Azure Active Directory integration with Autotask Workplace | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Autotask Workplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: cc1ee04c9d614e895c4e8a021564e9b9405fa8c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868404"
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="a47f7-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="a47f7-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="a47f7-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a47f7-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a47f7-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a47f7-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a47f7-106">You can control in Azure AD who has access to Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="a47f7-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="a47f7-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a47f7-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a47f7-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a47f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a47f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a47f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a47f7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a47f7-110">Prerequisites</span></span>

<span data-ttu-id="a47f7-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a47f7-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="a47f7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a47f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a47f7-113">An Autotask Workplace single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a47f7-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="a47f7-114">You must be an administrator or super administrator in Workplace.</span><span class="sxs-lookup"><span data-stu-id="a47f7-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="a47f7-115">You must have an administrator account in the Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a47f7-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="a47f7-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span><span class="sxs-lookup"><span data-stu-id="a47f7-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="a47f7-117">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a47f7-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a47f7-118">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a47f7-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a47f7-119">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a47f7-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a47f7-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a47f7-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a47f7-121">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a47f7-121">Scenario description</span></span>
<span data-ttu-id="a47f7-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a47f7-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a47f7-123">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a47f7-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a47f7-124">Adding Autotask Workplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="a47f7-124">Adding Autotask Workplace from the gallery</span></span>
1. <span data-ttu-id="a47f7-125">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a47f7-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="a47f7-126">Adding Autotask Workplace from the gallery</span><span class="sxs-lookup"><span data-stu-id="a47f7-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="a47f7-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a47f7-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a47f7-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a47f7-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a47f7-131">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a47f7-132">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-132">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a47f7-134">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a47f7-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a47f7-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a47f7-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![Autotask Workplace in the results list](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a47f7-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a47f7-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a47f7-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a47f7-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a47f7-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a47f7-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="a47f7-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a47f7-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="a47f7-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a47f7-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a47f7-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a47f7-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a47f7-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a47f7-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a47f7-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a47f7-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a47f7-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a47f7-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a47f7-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a47f7-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a47f7-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a47f7-149">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a47f7-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a47f7-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span><span class="sxs-lookup"><span data-stu-id="a47f7-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="a47f7-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="a47f7-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a47f7-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a47f7-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

1. <span data-ttu-id="a47f7-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span><span class="sxs-lookup"><span data-stu-id="a47f7-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![Autotask workplace Domain and URLs single sign-on information for IDP](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="a47f7-158">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-158">a.</span></span> <span data-ttu-id="a47f7-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a47f7-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="a47f7-160">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-160">b.</span></span> <span data-ttu-id="a47f7-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="a47f7-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

1. <span data-ttu-id="a47f7-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a47f7-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![Autotask workplace Domain and URLs single sign-on information for SP](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="a47f7-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="a47f7-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a47f7-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a47f7-165">These values are not real.</span></span> <span data-ttu-id="a47f7-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a47f7-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a47f7-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a47f7-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

1. <span data-ttu-id="a47f7-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a47f7-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

1. <span data-ttu-id="a47f7-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a47f7-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/autotaskworkplace-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a47f7-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="a47f7-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="a47f7-173">When configuring the IdP, a subdomain will need to be specified.</span><span class="sxs-lookup"><span data-stu-id="a47f7-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="a47f7-174">To confirm the correct subdomain, login to Workplace Online.</span><span class="sxs-lookup"><span data-stu-id="a47f7-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="a47f7-175">Once logged in, make note to the subdomain in the URL.</span><span class="sxs-lookup"><span data-stu-id="a47f7-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="a47f7-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span><span class="sxs-lookup"><span data-stu-id="a47f7-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

1. <span data-ttu-id="a47f7-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a47f7-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Autotask Single Sign-on configuration](./media/autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="a47f7-179">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-179">a.</span></span> <span data-ttu-id="a47f7-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a47f7-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="a47f7-181">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-181">b.</span></span> <span data-ttu-id="a47f7-182">Click **Enable SSO**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-182">Click **Enable SSO**.</span></span>
    
    ![Autotask Single Sign-on approve configuration](./media/autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="a47f7-184">c.</span><span class="sxs-lookup"><span data-stu-id="a47f7-184">c.</span></span> <span data-ttu-id="a47f7-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span><span class="sxs-lookup"><span data-stu-id="a47f7-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="a47f7-186">d.</span><span class="sxs-lookup"><span data-stu-id="a47f7-186">d.</span></span> <span data-ttu-id="a47f7-187">Click **Approve**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="a47f7-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span><span class="sxs-lookup"><span data-stu-id="a47f7-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="a47f7-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a47f7-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a47f7-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a47f7-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a47f7-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a47f7-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a47f7-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a47f7-192">Create an Azure AD test user</span></span>

<span data-ttu-id="a47f7-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a47f7-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a47f7-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a47f7-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/autotaskworkplace-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a47f7-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/autotaskworkplace-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a47f7-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a47f7-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/autotaskworkplace-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a47f7-202">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a47f7-202">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a47f7-204">a.</span><span class="sxs-lookup"><span data-stu-id="a47f7-204">a.</span></span> <span data-ttu-id="a47f7-205">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a47f7-206">b.</span><span class="sxs-lookup"><span data-stu-id="a47f7-206">b.</span></span> <span data-ttu-id="a47f7-207">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a47f7-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a47f7-208">c.</span><span class="sxs-lookup"><span data-stu-id="a47f7-208">c.</span></span> <span data-ttu-id="a47f7-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a47f7-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a47f7-210">d.</span><span class="sxs-lookup"><span data-stu-id="a47f7-210">d.</span></span> <span data-ttu-id="a47f7-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="a47f7-212">Create an Autotask Workplace test user</span><span class="sxs-lookup"><span data-stu-id="a47f7-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="a47f7-213">In this section, you create a user called Britta Simon in Autotask.</span><span class="sxs-lookup"><span data-stu-id="a47f7-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="a47f7-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span><span class="sxs-lookup"><span data-stu-id="a47f7-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a47f7-215">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a47f7-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="a47f7-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="a47f7-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a47f7-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a47f7-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="a47f7-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a47f7-221">In the applications list, select **Autotask Workplace**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![The Autotask Workplace link in the Applications list](./media/autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

1. <span data-ttu-id="a47f7-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a47f7-223">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a47f7-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a47f7-225">Click **Add** button.</span></span> <span data-ttu-id="a47f7-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a47f7-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a47f7-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a47f7-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a47f7-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a47f7-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a47f7-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a47f7-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a47f7-231">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a47f7-231">Test single sign-on</span></span>

<span data-ttu-id="a47f7-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a47f7-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a47f7-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span><span class="sxs-lookup"><span data-stu-id="a47f7-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="a47f7-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a47f7-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a47f7-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a47f7-235">Additional resources</span></span>

* [<span data-ttu-id="a47f7-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a47f7-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a47f7-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a47f7-237">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/autotaskworkplace-tutorial/tutorial_general_203.png

