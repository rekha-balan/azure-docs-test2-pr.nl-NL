---
title: 'Tutorial: Azure Active Directory integration with Skyhigh Networks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skyhigh Networks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 48d6ddd1-4d3e-4019-8234-5e5212684d9c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2018
ms.author: jeedes
ms.openlocfilehash: 40237946adf0e9cf30367fd0464a6c32572c3aaf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965820"
---
# <a name="tutorial-azure-active-directory-integration-with-skyhigh-networks"></a><span data-ttu-id="03284-103">Tutorial: Azure Active Directory integration with Skyhigh Networks</span><span class="sxs-lookup"><span data-stu-id="03284-103">Tutorial: Azure Active Directory integration with Skyhigh Networks</span></span>

<span data-ttu-id="03284-104">In this tutorial, you learn how to integrate Skyhigh Networks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03284-104">In this tutorial, you learn how to integrate Skyhigh Networks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03284-105">Integrating Skyhigh Networks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="03284-105">Integrating Skyhigh Networks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="03284-106">You can control in Azure AD who has access to Skyhigh Networks.</span><span class="sxs-lookup"><span data-stu-id="03284-106">You can control in Azure AD who has access to Skyhigh Networks.</span></span>
- <span data-ttu-id="03284-107">You can enable your users to automatically get signed-on to Skyhigh Networks (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="03284-107">You can enable your users to automatically get signed-on to Skyhigh Networks (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="03284-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03284-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="03284-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="03284-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03284-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="03284-110">Prerequisites</span></span>

<span data-ttu-id="03284-111">To configure Azure AD integration with Skyhigh Networks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="03284-111">To configure Azure AD integration with Skyhigh Networks, you need the following items:</span></span>

- <span data-ttu-id="03284-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="03284-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03284-113">A Skyhigh Networks single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="03284-113">A Skyhigh Networks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03284-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="03284-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03284-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="03284-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03284-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="03284-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03284-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03284-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03284-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="03284-118">Scenario description</span></span>
<span data-ttu-id="03284-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="03284-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03284-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="03284-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03284-121">Adding Skyhigh Networks from the gallery</span><span class="sxs-lookup"><span data-stu-id="03284-121">Adding Skyhigh Networks from the gallery</span></span>
1. <span data-ttu-id="03284-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03284-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skyhigh-networks-from-the-gallery"></a><span data-ttu-id="03284-123">Adding Skyhigh Networks from the gallery</span><span class="sxs-lookup"><span data-stu-id="03284-123">Adding Skyhigh Networks from the gallery</span></span>
<span data-ttu-id="03284-124">To configure the integration of Skyhigh Networks into Azure AD, you need to add Skyhigh Networks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="03284-124">To configure the integration of Skyhigh Networks into Azure AD, you need to add Skyhigh Networks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="03284-125">**To add Skyhigh Networks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03284-125">**To add Skyhigh Networks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="03284-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="03284-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="03284-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="03284-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="03284-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="03284-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="03284-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="03284-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="03284-133">In the search box, type **Skyhigh Networks**, select **Skyhigh Networks** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="03284-133">In the search box, type **Skyhigh Networks**, select **Skyhigh Networks** from result panel then click **Add** button to add the application.</span></span>

    ![Skyhigh Networks in the results list](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="03284-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03284-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="03284-136">In this section, you configure and test Azure AD single sign-on with Skyhigh Networks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="03284-136">In this section, you configure and test Azure AD single sign-on with Skyhigh Networks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03284-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skyhigh Networks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03284-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skyhigh Networks is to a user in Azure AD.</span></span> <span data-ttu-id="03284-138">In other words, a link relationship between an Azure AD user and the related user in Skyhigh Networks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="03284-138">In other words, a link relationship between an Azure AD user and the related user in Skyhigh Networks needs to be established.</span></span>

<span data-ttu-id="03284-139">To configure and test Azure AD single sign-on with Skyhigh Networks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="03284-139">To configure and test Azure AD single sign-on with Skyhigh Networks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="03284-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="03284-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="03284-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03284-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="03284-142">**[Create a Skyhigh Networks test user](#create-a-skyhigh-networks-test-user)** - to have a counterpart of Britta Simon in Skyhigh Networks that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="03284-142">**[Create a Skyhigh Networks test user](#create-a-skyhigh-networks-test-user)** - to have a counterpart of Britta Simon in Skyhigh Networks that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="03284-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03284-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="03284-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="03284-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="03284-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03284-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="03284-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skyhigh Networks application.</span><span class="sxs-lookup"><span data-stu-id="03284-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skyhigh Networks application.</span></span>

<span data-ttu-id="03284-147">**To configure Azure AD single sign-on with Skyhigh Networks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03284-147">**To configure Azure AD single sign-on with Skyhigh Networks, perform the following steps:**</span></span>

1. <span data-ttu-id="03284-148">In the Azure portal, on the **Skyhigh Networks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="03284-148">In the Azure portal, on the **Skyhigh Networks** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="03284-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03284-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_samlbase.png)

1. <span data-ttu-id="03284-152">On the **Skyhigh Networks Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="03284-152">On the **Skyhigh Networks Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Skyhigh Networks Domain and URLs single sign-on information](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_url.png)

    <span data-ttu-id="03284-154">a.</span><span class="sxs-lookup"><span data-stu-id="03284-154">a.</span></span> <span data-ttu-id="03284-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`</span><span class="sxs-lookup"><span data-stu-id="03284-155">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`</span></span>

    <span data-ttu-id="03284-156">b.</span><span class="sxs-lookup"><span data-stu-id="03284-156">b.</span></span> <span data-ttu-id="03284-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/response/saml-postlogin`</span><span class="sxs-lookup"><span data-stu-id="03284-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/response/saml-postlogin`</span></span>

1. <span data-ttu-id="03284-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="03284-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Skyhigh Networks Domain and URLs single sign-on information](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_url1.png)

    <span data-ttu-id="03284-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`</span><span class="sxs-lookup"><span data-stu-id="03284-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<ENV>.myshn.net/shndash/saml/Azure_SSO`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="03284-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="03284-161">These values are not real.</span></span> <span data-ttu-id="03284-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="03284-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="03284-163">Contact [Skyhigh Networks Client support team](mailto:support@skyhighnetworks.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="03284-163">Contact [Skyhigh Networks Client support team](mailto:support@skyhighnetworks.com) to get these values.</span></span> 

1. <span data-ttu-id="03284-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="03284-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_certificate.png) 

1. <span data-ttu-id="03284-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="03284-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/skyhighnetworks-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="03284-168">On the **Skyhigh Networks Configuration** section, click **Configure Skyhigh Networks** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="03284-168">On the **Skyhigh Networks Configuration** section, click **Configure Skyhigh Networks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="03284-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="03284-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Skyhigh Networks Configuration](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_configure.png) 

1. <span data-ttu-id="03284-171">To configure single sign-on on **Skyhigh Networks** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Skyhigh Networks support team](mailto:support@skyhighnetworks.com).</span><span class="sxs-lookup"><span data-stu-id="03284-171">To configure single sign-on on **Skyhigh Networks** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Skyhigh Networks support team](mailto:support@skyhighnetworks.com).</span></span> <span data-ttu-id="03284-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="03284-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="03284-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="03284-173">Create an Azure AD test user</span></span>

<span data-ttu-id="03284-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03284-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="03284-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03284-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="03284-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="03284-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/skyhighnetworks-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="03284-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="03284-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/skyhighnetworks-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="03284-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="03284-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/skyhighnetworks-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="03284-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="03284-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/skyhighnetworks-tutorial/create_aaduser_04.png)

    <span data-ttu-id="03284-185">a.</span><span class="sxs-lookup"><span data-stu-id="03284-185">a.</span></span> <span data-ttu-id="03284-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03284-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03284-187">b.</span><span class="sxs-lookup"><span data-stu-id="03284-187">b.</span></span> <span data-ttu-id="03284-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03284-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="03284-189">c.</span><span class="sxs-lookup"><span data-stu-id="03284-189">c.</span></span> <span data-ttu-id="03284-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="03284-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="03284-191">d.</span><span class="sxs-lookup"><span data-stu-id="03284-191">d.</span></span> <span data-ttu-id="03284-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="03284-192">Click **Create**.</span></span>
 
### <a name="create-a-skyhigh-networks-test-user"></a><span data-ttu-id="03284-193">Create a Skyhigh Networks test user</span><span class="sxs-lookup"><span data-stu-id="03284-193">Create a Skyhigh Networks test user</span></span>

<span data-ttu-id="03284-194">In this section, you create a user called Britta Simon in Skyhigh Networks.</span><span class="sxs-lookup"><span data-stu-id="03284-194">In this section, you create a user called Britta Simon in Skyhigh Networks.</span></span> <span data-ttu-id="03284-195">Work with [Skyhigh Networks support team](mailto:support@skyhighnetworks.com) to add the users in the Skyhigh Networks platform.</span><span class="sxs-lookup"><span data-stu-id="03284-195">Work with [Skyhigh Networks support team](mailto:support@skyhighnetworks.com) to add the users in the Skyhigh Networks platform.</span></span> <span data-ttu-id="03284-196">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="03284-196">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="03284-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="03284-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="03284-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skyhigh Networks.</span><span class="sxs-lookup"><span data-stu-id="03284-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skyhigh Networks.</span></span>

![Assign the user role][200] 

<span data-ttu-id="03284-200">**To assign Britta Simon to Skyhigh Networks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03284-200">**To assign Britta Simon to Skyhigh Networks, perform the following steps:**</span></span>

1. <span data-ttu-id="03284-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="03284-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="03284-203">In the applications list, select **Skyhigh Networks**.</span><span class="sxs-lookup"><span data-stu-id="03284-203">In the applications list, select **Skyhigh Networks**.</span></span>

    ![The Skyhigh Networks link in the Applications list](./media/skyhighnetworks-tutorial/tutorial_skyhighnetworks_app.png)  

1. <span data-ttu-id="03284-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="03284-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="03284-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="03284-207">Click **Add** button.</span></span> <span data-ttu-id="03284-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="03284-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="03284-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="03284-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="03284-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="03284-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="03284-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="03284-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="03284-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="03284-213">Test single sign-on</span></span>

<span data-ttu-id="03284-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="03284-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="03284-215">When you click the Skyhigh Networks tile in the Access Panel, you should get automatically signed-on to your Skyhigh Networks application.</span><span class="sxs-lookup"><span data-stu-id="03284-215">When you click the Skyhigh Networks tile in the Access Panel, you should get automatically signed-on to your Skyhigh Networks application.</span></span>
<span data-ttu-id="03284-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03284-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="03284-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="03284-217">Additional resources</span></span>

* [<span data-ttu-id="03284-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03284-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="03284-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03284-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skyhighnetworks-tutorial/tutorial_general_01.png
[2]: ./media/skyhighnetworks-tutorial/tutorial_general_02.png
[3]: ./media/skyhighnetworks-tutorial/tutorial_general_03.png
[4]: ./media/skyhighnetworks-tutorial/tutorial_general_04.png

[100]: ./media/skyhighnetworks-tutorial/tutorial_general_100.png

[200]: ./media/skyhighnetworks-tutorial/tutorial_general_200.png
[201]: ./media/skyhighnetworks-tutorial/tutorial_general_201.png
[202]: ./media/skyhighnetworks-tutorial/tutorial_general_202.png
[203]: ./media/skyhighnetworks-tutorial/tutorial_general_203.png

