---
title: 'Tutorial: Azure Active Directory integration with ContractWorks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ContractWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e7b269d6-3c4e-4bc4-a55f-5071d1f52591
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: ddf012f276a300cb8f70590c306020993b448cc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856644"
---
# <a name="tutorial-azure-active-directory-integration-with-contractworks"></a><span data-ttu-id="17610-103">Tutorial: Azure Active Directory integration with ContractWorks</span><span class="sxs-lookup"><span data-stu-id="17610-103">Tutorial: Azure Active Directory integration with ContractWorks</span></span>

<span data-ttu-id="17610-104">In this tutorial, you learn how to integrate ContractWorks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17610-104">In this tutorial, you learn how to integrate ContractWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17610-105">Integrating ContractWorks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="17610-105">Integrating ContractWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17610-106">You can control in Azure AD who has access to ContractWorks.</span><span class="sxs-lookup"><span data-stu-id="17610-106">You can control in Azure AD who has access to ContractWorks.</span></span>
- <span data-ttu-id="17610-107">You can enable your users to automatically get signed-on to ContractWorks (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="17610-107">You can enable your users to automatically get signed-on to ContractWorks (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="17610-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="17610-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="17610-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="17610-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17610-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="17610-110">Prerequisites</span></span>

<span data-ttu-id="17610-111">To configure Azure AD integration with ContractWorks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="17610-111">To configure Azure AD integration with ContractWorks, you need the following items:</span></span>

- <span data-ttu-id="17610-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="17610-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17610-113">A ContractWorks single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="17610-113">A ContractWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17610-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="17610-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17610-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="17610-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17610-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="17610-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17610-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17610-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17610-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="17610-118">Scenario description</span></span>
<span data-ttu-id="17610-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="17610-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17610-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="17610-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17610-121">Adding ContractWorks from the gallery</span><span class="sxs-lookup"><span data-stu-id="17610-121">Adding ContractWorks from the gallery</span></span>
1. <span data-ttu-id="17610-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17610-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-contractworks-from-the-gallery"></a><span data-ttu-id="17610-123">Adding ContractWorks from the gallery</span><span class="sxs-lookup"><span data-stu-id="17610-123">Adding ContractWorks from the gallery</span></span>
<span data-ttu-id="17610-124">To configure the integration of ContractWorks into Azure AD, you need to add ContractWorks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="17610-124">To configure the integration of ContractWorks into Azure AD, you need to add ContractWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17610-125">**To add ContractWorks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17610-125">**To add ContractWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17610-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="17610-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="17610-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="17610-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17610-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17610-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="17610-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="17610-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="17610-133">In the search box, type **ContractWorks**, select **ContractWorks** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="17610-133">In the search box, type **ContractWorks**, select **ContractWorks** from result panel then click **Add** button to add the application.</span></span>

    ![ContractWorks in the results list](./media/contractworks-tutorial/tutorial_contractworks_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="17610-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17610-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="17610-136">In this section, you configure and test Azure AD single sign-on with ContractWorks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17610-136">In this section, you configure and test Azure AD single sign-on with ContractWorks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17610-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ContractWorks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17610-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ContractWorks is to a user in Azure AD.</span></span> <span data-ttu-id="17610-138">In other words, a link relationship between an Azure AD user and the related user in ContractWorks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="17610-138">In other words, a link relationship between an Azure AD user and the related user in ContractWorks needs to be established.</span></span>

<span data-ttu-id="17610-139">To configure and test Azure AD single sign-on with ContractWorks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="17610-139">To configure and test Azure AD single sign-on with ContractWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17610-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="17610-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="17610-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17610-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="17610-142">**[Create a ContractWorks test user](#create-a-contractworks-test-user)** - to have a counterpart of Britta Simon in ContractWorks that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="17610-142">**[Create a ContractWorks test user](#create-a-contractworks-test-user)** - to have a counterpart of Britta Simon in ContractWorks that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="17610-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17610-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="17610-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="17610-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="17610-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17610-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="17610-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ContractWorks application.</span><span class="sxs-lookup"><span data-stu-id="17610-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ContractWorks application.</span></span>

<span data-ttu-id="17610-147">**To configure Azure AD single sign-on with ContractWorks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17610-147">**To configure Azure AD single sign-on with ContractWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="17610-148">In the Azure portal, on the **ContractWorks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="17610-148">In the Azure portal, on the **ContractWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="17610-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17610-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/contractworks-tutorial/tutorial_contractworks_samlbase.png)

1. <span data-ttu-id="17610-152">On the **ContractWorks Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="17610-152">On the **ContractWorks Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![ContractWorks Domain and URLs single sign-on information](./media/contractworks-tutorial/tutorial_contractworks_url.png)

    <span data-ttu-id="17610-154">In the **Identifier** textbox, type a URL: `https://login.securedocs.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="17610-154">In the **Identifier** textbox, type a URL: `https://login.securedocs.com/saml/metadata`</span></span>

1. <span data-ttu-id="17610-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="17610-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ContractWorks Domain and URLs single sign-on information](./media/contractworks-tutorial/tutorial_contractworks_url1.png)

    <span data-ttu-id="17610-157">In the **Sign-on URL** textbox, type a URL: `https://login.securedocs.com/saml/hint`</span><span class="sxs-lookup"><span data-stu-id="17610-157">In the **Sign-on URL** textbox, type a URL: `https://login.securedocs.com/saml/hint`</span></span>
     
1. <span data-ttu-id="17610-158">ContractWorks application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="17610-158">ContractWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="17610-159">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="17610-159">Configure the following claims for this application.</span></span> <span data-ttu-id="17610-160">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="17610-160">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="17610-161">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="17610-161">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/contractworks-tutorial/tutorial_ContractWorks_attribute.png)

1. <span data-ttu-id="17610-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17610-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="17610-164">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="17610-164">Attribute Name</span></span> | <span data-ttu-id="17610-165">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="17610-165">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="17610-166">mail</span><span class="sxs-lookup"><span data-stu-id="17610-166">mail</span></span> | <span data-ttu-id="17610-167">user.mail</span><span class="sxs-lookup"><span data-stu-id="17610-167">user.mail</span></span> |
    | <span data-ttu-id="17610-168">displayName</span><span class="sxs-lookup"><span data-stu-id="17610-168">displayName</span></span> | <span data-ttu-id="17610-169">user.displayname</span><span class="sxs-lookup"><span data-stu-id="17610-169">user.displayname</span></span> |

    <span data-ttu-id="17610-170">a.</span><span class="sxs-lookup"><span data-stu-id="17610-170">a.</span></span> <span data-ttu-id="17610-171">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="17610-171">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/contractworks-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/contractworks-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="17610-174">b.</span><span class="sxs-lookup"><span data-stu-id="17610-174">b.</span></span> <span data-ttu-id="17610-175">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="17610-175">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="17610-176">c.</span><span class="sxs-lookup"><span data-stu-id="17610-176">c.</span></span> <span data-ttu-id="17610-177">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="17610-177">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="17610-178">d.</span><span class="sxs-lookup"><span data-stu-id="17610-178">d.</span></span> <span data-ttu-id="17610-179">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="17610-179">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="17610-180">d.</span><span class="sxs-lookup"><span data-stu-id="17610-180">d.</span></span> <span data-ttu-id="17610-181">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="17610-181">Click **Ok**</span></span>

1. <span data-ttu-id="17610-182">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="17610-182">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/contractworks-tutorial/tutorial_metadataurl.png)
     
1. <span data-ttu-id="17610-184">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="17610-184">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/contractworks-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="17610-186">To configure single sign-on on **ContractWorks** side, you need to send the generated **App Federation Metadata Url** to [ContractWorks support team](mailto:support@contractworks.com).</span><span class="sxs-lookup"><span data-stu-id="17610-186">To configure single sign-on on **ContractWorks** side, you need to send the generated **App Federation Metadata Url** to [ContractWorks support team](mailto:support@contractworks.com).</span></span> <span data-ttu-id="17610-187">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="17610-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="17610-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17610-188">Create an Azure AD test user</span></span>

<span data-ttu-id="17610-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17610-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="17610-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17610-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17610-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="17610-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/contractworks-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="17610-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="17610-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/contractworks-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="17610-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="17610-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/contractworks-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="17610-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17610-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/contractworks-tutorial/create_aaduser_04.png)

    <span data-ttu-id="17610-200">a.</span><span class="sxs-lookup"><span data-stu-id="17610-200">a.</span></span> <span data-ttu-id="17610-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17610-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17610-202">b.</span><span class="sxs-lookup"><span data-stu-id="17610-202">b.</span></span> <span data-ttu-id="17610-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17610-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="17610-204">c.</span><span class="sxs-lookup"><span data-stu-id="17610-204">c.</span></span> <span data-ttu-id="17610-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="17610-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="17610-206">d.</span><span class="sxs-lookup"><span data-stu-id="17610-206">d.</span></span> <span data-ttu-id="17610-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="17610-207">Click **Create**.</span></span>
 
### <a name="create-a-contractworks-test-user"></a><span data-ttu-id="17610-208">Create a ContractWorks test user</span><span class="sxs-lookup"><span data-stu-id="17610-208">Create a ContractWorks test user</span></span>

<span data-ttu-id="17610-209">In this section, you create a user called Britta Simon in ContractWorks.</span><span class="sxs-lookup"><span data-stu-id="17610-209">In this section, you create a user called Britta Simon in ContractWorks.</span></span> <span data-ttu-id="17610-210">Work with [ContractWorks support team](mailto:support@contractworks.com) to add the users in the ContractWorks platform.</span><span class="sxs-lookup"><span data-stu-id="17610-210">Work with [ContractWorks support team](mailto:support@contractworks.com) to add the users in the ContractWorks platform.</span></span> <span data-ttu-id="17610-211">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17610-211">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="17610-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17610-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="17610-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ContractWorks.</span><span class="sxs-lookup"><span data-stu-id="17610-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ContractWorks.</span></span>

![Assign the user role][200] 

<span data-ttu-id="17610-215">**To assign Britta Simon to ContractWorks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17610-215">**To assign Britta Simon to ContractWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="17610-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17610-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="17610-218">In the applications list, select **ContractWorks**.</span><span class="sxs-lookup"><span data-stu-id="17610-218">In the applications list, select **ContractWorks**.</span></span>

    ![The ContractWorks link in the Applications list](./media/contractworks-tutorial/tutorial_contractworks_app.png)  

1. <span data-ttu-id="17610-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="17610-220">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="17610-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="17610-222">Click **Add** button.</span></span> <span data-ttu-id="17610-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17610-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="17610-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="17610-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="17610-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="17610-226">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="17610-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17610-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="17610-228">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="17610-228">Test single sign-on</span></span>

<span data-ttu-id="17610-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="17610-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="17610-230">When you click the ContractWorks tile in the Access Panel, you should get automatically signed-on to your ContractWorks application.</span><span class="sxs-lookup"><span data-stu-id="17610-230">When you click the ContractWorks tile in the Access Panel, you should get automatically signed-on to your ContractWorks application.</span></span>
<span data-ttu-id="17610-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17610-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17610-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="17610-232">Additional resources</span></span>

* [<span data-ttu-id="17610-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17610-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="17610-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17610-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/contractworks-tutorial/tutorial_general_01.png
[2]: ./media/contractworks-tutorial/tutorial_general_02.png
[3]: ./media/contractworks-tutorial/tutorial_general_03.png
[4]: ./media/contractworks-tutorial/tutorial_general_04.png

[100]: ./media/contractworks-tutorial/tutorial_general_100.png

[200]: ./media/contractworks-tutorial/tutorial_general_200.png
[201]: ./media/contractworks-tutorial/tutorial_general_201.png
[202]: ./media/contractworks-tutorial/tutorial_general_202.png
[203]: ./media/contractworks-tutorial/tutorial_general_203.png

