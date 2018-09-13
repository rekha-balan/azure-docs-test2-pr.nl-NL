---
title: 'Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dbf21c7c22a9b3273a65f7e186a2ac02ccae6ba2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967721"
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="6b6dd-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6b6dd-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="6b6dd-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="6b6dd-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b6dd-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="6b6dd-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="6b6dd-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="6b6dd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6b6dd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b6dd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6b6dd-110">Prerequisites</span></span>

<span data-ttu-id="6b6dd-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="6b6dd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6b6dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b6dd-113">A Symantec Web Security Service (WSS) account</span><span class="sxs-lookup"><span data-stu-id="6b6dd-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="6b6dd-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="6b6dd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b6dd-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="6b6dd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b6dd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b6dd-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6b6dd-118">Scenario description</span></span>
<span data-ttu-id="6b6dd-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="6b6dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b6dd-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span><span class="sxs-lookup"><span data-stu-id="6b6dd-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
1. <span data-ttu-id="6b6dd-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6b6dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="6b6dd-123">Adding Symantec Web Security Service (WSS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="6b6dd-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="6b6dd-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b6dd-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6b6dd-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b6dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="6b6dd-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b6dd-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="6b6dd-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="6b6dd-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web Security Service (WSS) in the results list](./media/symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6b6dd-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6b6dd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6b6dd-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6b6dd-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b6dd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="6b6dd-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="6b6dd-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b6dd-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b6dd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6b6dd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6b6dd-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6b6dd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6b6dd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6b6dd-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6b6dd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6b6dd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="6b6dd-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6b6dd-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="6b6dd-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="6b6dd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

1. <span data-ttu-id="6b6dd-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Symantec Web Security Service (WSS) Domain and URLs single sign-on information](./media/symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="6b6dd-155">a.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-155">a.</span></span> <span data-ttu-id="6b6dd-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="6b6dd-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="6b6dd-157">b.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-157">b.</span></span> <span data-ttu-id="6b6dd-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="6b6dd-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b6dd-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

1. <span data-ttu-id="6b6dd-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

1. <span data-ttu-id="6b6dd-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/symantec-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="6b6dd-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="6b6dd-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="6b6dd-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="6b6dd-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6b6dd-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b6dd-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b6dd-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b6dd-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6b6dd-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6b6dd-170">Create an Azure AD test user</span></span>

<span data-ttu-id="6b6dd-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6b6dd-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6b6dd-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b6dd-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/symantec-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="6b6dd-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/symantec-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="6b6dd-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/symantec-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="6b6dd-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6b6dd-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6b6dd-182">a.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-182">a.</span></span> <span data-ttu-id="6b6dd-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b6dd-184">b.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-184">b.</span></span> <span data-ttu-id="6b6dd-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6b6dd-186">c.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-186">c.</span></span> <span data-ttu-id="6b6dd-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6b6dd-188">d.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-188">d.</span></span> <span data-ttu-id="6b6dd-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="6b6dd-190">Create a Symantec Web Security Service (WSS) test user</span><span class="sxs-lookup"><span data-stu-id="6b6dd-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="6b6dd-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6b6dd-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="6b6dd-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span><span class="sxs-lookup"><span data-stu-id="6b6dd-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="6b6dd-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="6b6dd-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6b6dd-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6b6dd-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6b6dd-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="6b6dd-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6b6dd-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Assign the user role][200] 

<span data-ttu-id="6b6dd-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6b6dd-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="6b6dd-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6b6dd-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![The Symantec Web Security Service (WSS) link in the Applications list](./media/symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

1. <span data-ttu-id="6b6dd-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-204">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="6b6dd-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-206">Click **Add** button.</span></span> <span data-ttu-id="6b6dd-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="6b6dd-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6b6dd-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6b6dd-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6b6dd-212">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6b6dd-212">Test single sign-on</span></span>

<span data-ttu-id="6b6dd-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="6b6dd-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="6b6dd-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="6b6dd-216">Once authenticated, you'll be able to browse to the website that you chose.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="6b6dd-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b6dd-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b6dd-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6b6dd-218">Additional resources</span></span>

* [<span data-ttu-id="6b6dd-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b6dd-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6b6dd-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b6dd-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/symantec-tutorial/tutorial_general_01.png
[2]: ./media/symantec-tutorial/tutorial_general_02.png
[3]: ./media/symantec-tutorial/tutorial_general_03.png
[4]: ./media/symantec-tutorial/tutorial_general_04.png

[100]: ./media/symantec-tutorial/tutorial_general_100.png

[200]: ./media/symantec-tutorial/tutorial_general_200.png
[201]: ./media/symantec-tutorial/tutorial_general_201.png
[202]: ./media/symantec-tutorial/tutorial_general_202.png
[203]: ./media/symantec-tutorial/tutorial_general_203.png

