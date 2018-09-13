---
title: 'Tutorial: Azure Active Directory integration with Huddle | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Huddle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: jeedes
ms.openlocfilehash: 08114fc52665eb336844a1072df8bd3f2591dd07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864793"
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="6a421-103">Tutorial: Azure Active Directory integration with Huddle</span><span class="sxs-lookup"><span data-stu-id="6a421-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="6a421-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a421-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a421-105">Integrating Huddle with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6a421-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a421-106">You can control in Azure AD who has access to Huddle</span><span class="sxs-lookup"><span data-stu-id="6a421-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="6a421-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6a421-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a421-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a421-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a421-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6a421-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a421-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a421-110">Prerequisites</span></span>

<span data-ttu-id="6a421-111">To configure Azure AD integration with Huddle, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6a421-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="6a421-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6a421-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a421-113">A Huddle single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6a421-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a421-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6a421-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a421-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6a421-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a421-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6a421-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a421-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a421-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a421-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6a421-118">Scenario description</span></span>

<span data-ttu-id="6a421-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6a421-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a421-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a421-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a421-121">Adding Huddle from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a421-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="6a421-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a421-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="6a421-123">Adding Huddle from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a421-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="6a421-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6a421-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a421-125">**To add Huddle from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a421-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a421-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6a421-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a421-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6a421-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a421-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6a421-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6a421-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6a421-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6a421-133">In the search box, type **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="6a421-133">In the search box, type **Huddle**.</span></span>

    ![Creating an Azure AD test user](./media/huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="6a421-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6a421-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a421-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a421-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="6a421-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6a421-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a421-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a421-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="6a421-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6a421-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="6a421-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6a421-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a421-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a421-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a421-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6a421-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="6a421-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a421-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="6a421-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6a421-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="6a421-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a421-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="6a421-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6a421-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a421-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a421-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a421-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span><span class="sxs-lookup"><span data-stu-id="6a421-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="6a421-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a421-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="6a421-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6a421-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="6a421-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a421-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="6a421-155">On the **Huddle Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6a421-155">On the **Huddle Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Huddle Domain and URLs single sign-on information](./media/huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="6a421-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a421-157">a.</span></span> <span data-ttu-id="6a421-158">In the **Identifier** textbox, type any one of the URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="6a421-158">In the **Identifier** textbox, type any one of the URL using the following pattern:</span></span>

    | | |
    |--|--|
    | `https://<customsubdomain>.huddle.com`|
    | `https://us.huddle.com` |
    | |

    <span data-ttu-id="6a421-159">b.</span><span class="sxs-lookup"><span data-stu-id="6a421-159">b.</span></span> <span data-ttu-id="6a421-160">In the **Reply URL** textbox, type any one of the URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="6a421-160">In the **Reply URL** textbox, type any one of the URL using the following pattern:</span></span>

    | | |
    |--|--|
    | `https://<customsubdomain>.huddle.com/saml/idp-initiated-sso`|
    | `https://us.huddle.com/saml/idp-initiated-sso`|
    | |

4. <span data-ttu-id="6a421-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6a421-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Huddle Domain and URLs single sign-on information](./media/huddle-tutorial/tutorial_huddle_url1.png)

    <span data-ttu-id="6a421-163">In the **Sign-on URL** textbox, type any one of the URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="6a421-163">In the **Sign-on URL** textbox, type any one of the URL using the following pattern:</span></span>
    
    | | |
    |--|--|
    | `https://<customsubdomain>.huddle.com`|
    | `https://us.huddle.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="6a421-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6a421-164">These values are not real.</span></span> <span data-ttu-id="6a421-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="6a421-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="6a421-166">Contact [Huddle Client support team](https://huddle.zendesk.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6a421-166">Contact [Huddle Client support team](https://huddle.zendesk.com) to get these values.</span></span> 

5. <span data-ttu-id="6a421-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6a421-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/huddle-tutorial/tutorial_huddle_certificate.png) 

6. <span data-ttu-id="6a421-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6a421-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/huddle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6a421-171">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6a421-171">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a421-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="6a421-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Configure Single Sign-On](./media/huddle-tutorial/tutorial_huddle_configure.png) 
    
8. <span data-ttu-id="6a421-174">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="6a421-174">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="6a421-175">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="6a421-175">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="6a421-176">Single sign-on needs to be enabled by the Huddle support team.</span><span class="sxs-lookup"><span data-stu-id="6a421-176">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="6a421-177">You get a notification when the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="6a421-177">You get a notification when the configuration has been completed.</span></span> 
    > 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a421-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a421-178">Creating an Azure AD test user</span></span>

<span data-ttu-id="6a421-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a421-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6a421-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a421-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a421-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6a421-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a421-184">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6a421-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a421-186">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6a421-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a421-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a421-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a421-190">a.</span><span class="sxs-lookup"><span data-stu-id="6a421-190">a.</span></span> <span data-ttu-id="6a421-191">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a421-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a421-192">b.</span><span class="sxs-lookup"><span data-stu-id="6a421-192">b.</span></span> <span data-ttu-id="6a421-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a421-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a421-194">c.</span><span class="sxs-lookup"><span data-stu-id="6a421-194">c.</span></span> <span data-ttu-id="6a421-195">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6a421-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a421-196">d.</span><span class="sxs-lookup"><span data-stu-id="6a421-196">d.</span></span> <span data-ttu-id="6a421-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a421-197">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="6a421-198">Creating a Huddle test user</span><span class="sxs-lookup"><span data-stu-id="6a421-198">Creating a Huddle test user</span></span>

<span data-ttu-id="6a421-199">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span><span class="sxs-lookup"><span data-stu-id="6a421-199">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="6a421-200">In the case of Huddle, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="6a421-200">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="6a421-201">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a421-201">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6a421-202">Log in to your **Huddle** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="6a421-202">Log in to your **Huddle** company site as administrator.</span></span>

2. <span data-ttu-id="6a421-203">Click **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="6a421-203">Click **Workspace**.</span></span>

3. <span data-ttu-id="6a421-204">Click **People \> Invite People**.</span><span class="sxs-lookup"><span data-stu-id="6a421-204">Click **People \> Invite People**.</span></span>
   
    <span data-ttu-id="6a421-205">![People](./media/huddle-tutorial/IC787838.png "People")</span><span class="sxs-lookup"><span data-stu-id="6a421-205">![People](./media/huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="6a421-206">In the **Create a new invitation** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a421-206">In the **Create a new invitation** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6a421-207">![New Invitation](./media/huddle-tutorial/IC787839.png "New Invitation")</span><span class="sxs-lookup"><span data-stu-id="6a421-207">![New Invitation](./media/huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
    <span data-ttu-id="6a421-208">a.</span><span class="sxs-lookup"><span data-stu-id="6a421-208">a.</span></span> <span data-ttu-id="6a421-209">In the **Choose a team to invite people to join** list, select **team**.</span><span class="sxs-lookup"><span data-stu-id="6a421-209">In the **Choose a team to invite people to join** list, select **team**.</span></span>

    <span data-ttu-id="6a421-210">b.</span><span class="sxs-lookup"><span data-stu-id="6a421-210">b.</span></span> <span data-ttu-id="6a421-211">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span><span class="sxs-lookup"><span data-stu-id="6a421-211">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

    <span data-ttu-id="6a421-212">c.</span><span class="sxs-lookup"><span data-stu-id="6a421-212">c.</span></span> <span data-ttu-id="6a421-213">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="6a421-213">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="6a421-214">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="6a421-214">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="6a421-215">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6a421-215">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a421-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a421-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a421-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span><span class="sxs-lookup"><span data-stu-id="6a421-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Assign User][200] 

<span data-ttu-id="6a421-219">**To assign Britta Simon to Huddle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a421-219">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="6a421-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6a421-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="6a421-222">In the applications list, select **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="6a421-222">In the applications list, select **Huddle**.</span></span>

    ![Configure Single Sign-On](./media/huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="6a421-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6a421-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="6a421-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6a421-226">Click **Add** button.</span></span> <span data-ttu-id="6a421-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a421-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="6a421-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6a421-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a421-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a421-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a421-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a421-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a421-232">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a421-232">Testing single sign-on</span></span>

<span data-ttu-id="6a421-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6a421-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a421-234">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span><span class="sxs-lookup"><span data-stu-id="6a421-234">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="6a421-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a421-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a421-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6a421-236">Additional resources</span></span>

* [<span data-ttu-id="6a421-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a421-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6a421-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a421-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/huddle-tutorial/tutorial_general_01.png
[2]: ./media/huddle-tutorial/tutorial_general_02.png
[3]: ./media/huddle-tutorial/tutorial_general_03.png
[4]: ./media/huddle-tutorial/tutorial_general_04.png
[100]: ./media/huddle-tutorial/tutorial_general_100.png
[200]: ./media/huddle-tutorial/tutorial_general_200.png
[201]: ./media/huddle-tutorial/tutorial_general_201.png
[202]: ./media/huddle-tutorial/tutorial_general_202.png
[203]: ./media/huddle-tutorial/tutorial_general_203.png
