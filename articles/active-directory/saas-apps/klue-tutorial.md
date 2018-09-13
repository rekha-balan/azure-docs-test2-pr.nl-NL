---
title: 'Tutorial: Azure Active Directory integration with Klue | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Klue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2018
ms.author: jeedes
ms.openlocfilehash: 4afe11d6d241e86b57ebb40d54e4c2dceb63a46c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869790"
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="ecb55-103">Tutorial: Azure Active Directory integration with Klue</span><span class="sxs-lookup"><span data-stu-id="ecb55-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="ecb55-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecb55-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecb55-105">Integrating Klue with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ecb55-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ecb55-106">You can control in Azure AD who has access to Klue</span><span class="sxs-lookup"><span data-stu-id="ecb55-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="ecb55-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ecb55-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecb55-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ecb55-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ecb55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ecb55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecb55-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ecb55-110">Prerequisites</span></span>

<span data-ttu-id="ecb55-111">To configure Azure AD integration with Klue, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ecb55-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="ecb55-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ecb55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecb55-113">A Klue single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ecb55-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecb55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ecb55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecb55-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ecb55-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecb55-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ecb55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecb55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecb55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecb55-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ecb55-118">Scenario description</span></span>

<span data-ttu-id="ecb55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ecb55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecb55-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ecb55-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecb55-121">Adding Klue from the gallery</span><span class="sxs-lookup"><span data-stu-id="ecb55-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="ecb55-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecb55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="ecb55-123">Adding Klue from the gallery</span><span class="sxs-lookup"><span data-stu-id="ecb55-123">Adding Klue from the gallery</span></span>

<span data-ttu-id="ecb55-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ecb55-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ecb55-125">**To add Klue from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecb55-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ecb55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ecb55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecb55-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ecb55-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="ecb55-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ecb55-133">In the search box, type **Klue**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-133">In the search box, type **Klue**.</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="ecb55-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ecb55-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecb55-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecb55-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ecb55-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ecb55-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ecb55-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecb55-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="ecb55-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ecb55-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="ecb55-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ecb55-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ecb55-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ecb55-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ecb55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ecb55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ecb55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecb55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecb55-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ecb55-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ecb55-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ecb55-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecb55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ecb55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecb55-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecb55-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecb55-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span><span class="sxs-lookup"><span data-stu-id="ecb55-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="ecb55-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecb55-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="ecb55-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="ecb55-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ecb55-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="ecb55-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ecb55-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="ecb55-157">a.</span><span class="sxs-lookup"><span data-stu-id="ecb55-157">a.</span></span> <span data-ttu-id="ecb55-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="ecb55-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="ecb55-159">b.</span><span class="sxs-lookup"><span data-stu-id="ecb55-159">b.</span></span> <span data-ttu-id="ecb55-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="ecb55-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="ecb55-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ecb55-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="ecb55-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="ecb55-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="ecb55-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecb55-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ecb55-165">These values are not real.</span></span> <span data-ttu-id="ecb55-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="ecb55-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="ecb55-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ecb55-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="ecb55-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="ecb55-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ecb55-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="ecb55-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/attribute.png)

6. <span data-ttu-id="ecb55-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ecb55-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="ecb55-172">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ecb55-172">Attribute Name</span></span>      | <span data-ttu-id="ecb55-173">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ecb55-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="ecb55-174">first_name</span><span class="sxs-lookup"><span data-stu-id="ecb55-174">first_name</span></span>          | <span data-ttu-id="ecb55-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ecb55-175">user.givenname</span></span> |
    | <span data-ttu-id="ecb55-176">last_name</span><span class="sxs-lookup"><span data-stu-id="ecb55-176">last_name</span></span>           | <span data-ttu-id="ecb55-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="ecb55-177">user.surname</span></span> |
    | <span data-ttu-id="ecb55-178">email</span><span class="sxs-lookup"><span data-stu-id="ecb55-178">email</span></span>               | <span data-ttu-id="ecb55-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ecb55-179">user.userprincipalname</span></span>|

    <span data-ttu-id="ecb55-180">a.</span><span class="sxs-lookup"><span data-stu-id="ecb55-180">a.</span></span> <span data-ttu-id="ecb55-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ecb55-184">b.</span><span class="sxs-lookup"><span data-stu-id="ecb55-184">b.</span></span> <span data-ttu-id="ecb55-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ecb55-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ecb55-186">c.</span><span class="sxs-lookup"><span data-stu-id="ecb55-186">c.</span></span> <span data-ttu-id="ecb55-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ecb55-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ecb55-188">d.</span><span class="sxs-lookup"><span data-stu-id="ecb55-188">d.</span></span> <span data-ttu-id="ecb55-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-189">Click **Ok**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecb55-190">Please leave the **Namespace** value blank.</span><span class="sxs-lookup"><span data-stu-id="ecb55-190">Please leave the **Namespace** value blank.</span></span>

7. <span data-ttu-id="ecb55-191">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ecb55-191">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="ecb55-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ecb55-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ecb55-195">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ecb55-195">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ecb55-196">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="ecb55-196">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="ecb55-198">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="ecb55-198">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecb55-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ecb55-199">Creating an Azure AD test user</span></span>

<span data-ttu-id="ecb55-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecb55-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ecb55-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecb55-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ecb55-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ecb55-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ecb55-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ecb55-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ecb55-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ecb55-209">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecb55-211">a.</span><span class="sxs-lookup"><span data-stu-id="ecb55-211">a.</span></span> <span data-ttu-id="ecb55-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecb55-213">b.</span><span class="sxs-lookup"><span data-stu-id="ecb55-213">b.</span></span> <span data-ttu-id="ecb55-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ecb55-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecb55-215">c.</span><span class="sxs-lookup"><span data-stu-id="ecb55-215">c.</span></span> <span data-ttu-id="ecb55-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ecb55-217">d.</span><span class="sxs-lookup"><span data-stu-id="ecb55-217">d.</span></span> <span data-ttu-id="ecb55-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-218">Click **Create**.</span></span>

### <a name="creating-a-klue-test-user"></a><span data-ttu-id="ecb55-219">Creating a Klue test user</span><span class="sxs-lookup"><span data-stu-id="ecb55-219">Creating a Klue test user</span></span>

<span data-ttu-id="ecb55-220">The objective of this section is to create a user called Britta Simon in Klue.</span><span class="sxs-lookup"><span data-stu-id="ecb55-220">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="ecb55-221">Klue supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ecb55-221">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ecb55-222">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ecb55-222">There is no action item for you in this section.</span></span> <span data-ttu-id="ecb55-223">A new user is created during an attempt to access Klue if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ecb55-223">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="ecb55-224">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="ecb55-224">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ecb55-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ecb55-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ecb55-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span><span class="sxs-lookup"><span data-stu-id="ecb55-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![Assign User][200] 

<span data-ttu-id="ecb55-228">**To assign Britta Simon to Klue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ecb55-228">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="ecb55-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="ecb55-231">In the applications list, select **Klue**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-231">In the applications list, select **Klue**.</span></span>

    ![Configure Single Sign-On](./media/klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="ecb55-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ecb55-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

4. <span data-ttu-id="ecb55-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ecb55-235">Click **Add** button.</span></span> <span data-ttu-id="ecb55-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="ecb55-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ecb55-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ecb55-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecb55-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ecb55-240">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ecb55-241">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ecb55-241">Testing single sign-on</span></span>

<span data-ttu-id="ecb55-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ecb55-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ecb55-243">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span><span class="sxs-lookup"><span data-stu-id="ecb55-243">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="ecb55-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ecb55-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ecb55-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ecb55-245">Additional resources</span></span>

* [<span data-ttu-id="ecb55-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecb55-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ecb55-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ecb55-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/klue-tutorial/tutorial_general_01.png
[2]: ./media/klue-tutorial/tutorial_general_02.png
[3]: ./media/klue-tutorial/tutorial_general_03.png
[4]: ./media/klue-tutorial/tutorial_general_04.png

[100]: ./media/klue-tutorial/tutorial_general_100.png

[200]: ./media/klue-tutorial/tutorial_general_200.png
[201]: ./media/klue-tutorial/tutorial_general_201.png
[202]: ./media/klue-tutorial/tutorial_general_202.png
[203]: ./media/klue-tutorial/tutorial_general_203.png