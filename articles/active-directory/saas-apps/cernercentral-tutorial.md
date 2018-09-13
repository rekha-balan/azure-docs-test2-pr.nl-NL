---
title: 'Tutorial: Azure Active Directory integration with Cerner Central | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cerner Central.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jeedes
ms.openlocfilehash: 400aa0a50c0f05937011adf62f76d1d96fde3fc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865483"
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="403b9-103">Tutorial: Azure Active Directory integration with Cerner Central</span><span class="sxs-lookup"><span data-stu-id="403b9-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="403b9-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="403b9-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="403b9-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="403b9-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="403b9-106">You can control in Azure AD who has access to Cerner Central</span><span class="sxs-lookup"><span data-stu-id="403b9-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="403b9-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="403b9-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="403b9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="403b9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="403b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="403b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="403b9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="403b9-110">Prerequisites</span></span>

<span data-ttu-id="403b9-111">To configure Azure AD integration with Cerner Central, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="403b9-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="403b9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="403b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="403b9-113">An approved Cerner Central System Account</span><span class="sxs-lookup"><span data-stu-id="403b9-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="403b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="403b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="403b9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="403b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="403b9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="403b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="403b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="403b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="403b9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="403b9-118">Scenario description</span></span>
<span data-ttu-id="403b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="403b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="403b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="403b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="403b9-121">Adding Cerner Central from the gallery</span><span class="sxs-lookup"><span data-stu-id="403b9-121">Adding Cerner Central from the gallery</span></span>
1. <span data-ttu-id="403b9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="403b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="403b9-123">Adding Cerner Central from the gallery</span><span class="sxs-lookup"><span data-stu-id="403b9-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="403b9-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="403b9-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="403b9-125">**To add Cerner Central from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="403b9-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="403b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="403b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="403b9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="403b9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="403b9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="403b9-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="403b9-131">To add new application, click **New application** button on top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="403b9-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="403b9-133">In the search box, type **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="403b9-133">In the search box, type **Cerner Central**.</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/tutorial_cernercentral_search.png)

1. <span data-ttu-id="403b9-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="403b9-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="403b9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="403b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="403b9-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="403b9-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="403b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="403b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="403b9-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span><span class="sxs-lookup"><span data-stu-id="403b9-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="403b9-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="403b9-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="403b9-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="403b9-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="403b9-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="403b9-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="403b9-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="403b9-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
1. <span data-ttu-id="403b9-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="403b9-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="403b9-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="403b9-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="403b9-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="403b9-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="403b9-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span><span class="sxs-lookup"><span data-stu-id="403b9-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="403b9-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="403b9-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="403b9-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="403b9-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="403b9-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="403b9-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

1. <span data-ttu-id="403b9-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="403b9-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="403b9-156">a.</span><span class="sxs-lookup"><span data-stu-id="403b9-156">a.</span></span> <span data-ttu-id="403b9-157">In the **Identifier** textbox, type the value using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="403b9-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>

    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    
    <span data-ttu-id="403b9-158">b.</span><span class="sxs-lookup"><span data-stu-id="403b9-158">b.</span></span> <span data-ttu-id="403b9-159">In the **Reply URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="403b9-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/sso` |

    > [!NOTE]
    > <span data-ttu-id="403b9-160">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="403b9-160">These values are not the real.</span></span> <span data-ttu-id="403b9-161">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="403b9-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="403b9-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span><span class="sxs-lookup"><span data-stu-id="403b9-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>

1. <span data-ttu-id="403b9-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="403b9-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_metadataurl.png)

1. <span data-ttu-id="403b9-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="403b9-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="403b9-167">To configure single sign-on on **Cerner Central** side, you need to send the **App Federation Metadata Url** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="403b9-167">To configure single sign-on on **Cerner Central** side, you need to send the **App Federation Metadata Url** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="403b9-168">They configure the SSO on application side to complete the integration.</span><span class="sxs-lookup"><span data-stu-id="403b9-168">They configure the SSO on application side to complete the integration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="403b9-169">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="403b9-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="403b9-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="403b9-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="403b9-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="403b9-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="403b9-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="403b9-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="403b9-175">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="403b9-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="403b9-177">To open the **User** dialog, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="403b9-177">To open the **User** dialog, click **Add**.</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="403b9-179">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="403b9-179">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="403b9-181">a.</span><span class="sxs-lookup"><span data-stu-id="403b9-181">a.</span></span> <span data-ttu-id="403b9-182">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="403b9-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="403b9-183">b.</span><span class="sxs-lookup"><span data-stu-id="403b9-183">b.</span></span> <span data-ttu-id="403b9-184">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="403b9-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="403b9-185">c.</span><span class="sxs-lookup"><span data-stu-id="403b9-185">c.</span></span> <span data-ttu-id="403b9-186">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="403b9-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="403b9-187">d.</span><span class="sxs-lookup"><span data-stu-id="403b9-187">d.</span></span> <span data-ttu-id="403b9-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="403b9-188">Click **Create**.</span></span>

### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="403b9-189">Creating a Cerner Central test user</span><span class="sxs-lookup"><span data-stu-id="403b9-189">Creating a Cerner Central test user</span></span>

<span data-ttu-id="403b9-190">**Cerner Central** application allows authentication from any federated identity provider.</span><span class="sxs-lookup"><span data-stu-id="403b9-190">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="403b9-191">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span><span class="sxs-lookup"><span data-stu-id="403b9-191">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span> <span data-ttu-id="403b9-192">You can find more details [here](cernercentral-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="403b9-192">You can find more details [here](cernercentral-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="403b9-193">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="403b9-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="403b9-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="403b9-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Assign User][200]

<span data-ttu-id="403b9-196">**To assign Britta Simon to Cerner Central, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="403b9-196">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="403b9-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="403b9-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="403b9-199">In the applications list, select **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="403b9-199">In the applications list, select **Cerner Central**.</span></span>

    ![Configure Single Sign-On](./media/cernercentral-tutorial/tutorial_cernercentral_app.png)

1. <span data-ttu-id="403b9-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="403b9-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="403b9-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="403b9-203">Click **Add** button.</span></span> <span data-ttu-id="403b9-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="403b9-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="403b9-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="403b9-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="403b9-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="403b9-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="403b9-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="403b9-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="403b9-209">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="403b9-209">Testing single sign-on</span></span>

<span data-ttu-id="403b9-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="403b9-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="403b9-211">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span><span class="sxs-lookup"><span data-stu-id="403b9-211">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="403b9-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="403b9-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="403b9-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="403b9-213">Additional resources</span></span>

* [<span data-ttu-id="403b9-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="403b9-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="403b9-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="403b9-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="403b9-216">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="403b9-216">Configure User Provisioning</span></span>](cernercentral-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/cernercentral-tutorial/tutorial_general_203.png