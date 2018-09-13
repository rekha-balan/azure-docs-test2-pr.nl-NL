---
title: 'Tutorial: Azure Active Directory integration with Nuclino | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nuclino.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 74bbab82-5581-4dcf-8806-78f77c746968
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2018
ms.author: jeedes
ms.openlocfilehash: 1a5346b98de48b1a2f8928c3c2bf30730588e9c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866874"
---
# <a name="tutorial-azure-active-directory-integration-with-nuclino"></a><span data-ttu-id="b7a85-103">Tutorial: Azure Active Directory integration with Nuclino</span><span class="sxs-lookup"><span data-stu-id="b7a85-103">Tutorial: Azure Active Directory integration with Nuclino</span></span>

<span data-ttu-id="b7a85-104">In this tutorial, you learn how to integrate Nuclino with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7a85-104">In this tutorial, you learn how to integrate Nuclino with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7a85-105">Integrating Nuclino with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b7a85-105">Integrating Nuclino with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7a85-106">You can control in Azure AD who has access to Nuclino.</span><span class="sxs-lookup"><span data-stu-id="b7a85-106">You can control in Azure AD who has access to Nuclino.</span></span>
- <span data-ttu-id="b7a85-107">You can enable your users to automatically get signed-on to Nuclino (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b7a85-107">You can enable your users to automatically get signed-on to Nuclino (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b7a85-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7a85-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b7a85-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="b7a85-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a85-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7a85-110">Prerequisites</span></span>

<span data-ttu-id="b7a85-111">To configure Azure AD integration with Nuclino, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b7a85-111">To configure Azure AD integration with Nuclino, you need the following items:</span></span>

- <span data-ttu-id="b7a85-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b7a85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7a85-113">A Nuclino single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b7a85-113">A Nuclino single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7a85-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b7a85-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7a85-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b7a85-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7a85-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b7a85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7a85-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7a85-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7a85-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b7a85-118">Scenario description</span></span>

<span data-ttu-id="b7a85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b7a85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7a85-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7a85-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7a85-121">Adding Nuclino from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7a85-121">Adding Nuclino from the gallery</span></span>
2. <span data-ttu-id="b7a85-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7a85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nuclino-from-the-gallery"></a><span data-ttu-id="b7a85-123">Adding Nuclino from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7a85-123">Adding Nuclino from the gallery</span></span>

<span data-ttu-id="b7a85-124">To configure the integration of Nuclino into Azure AD, you need to add Nuclino from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b7a85-124">To configure the integration of Nuclino into Azure AD, you need to add Nuclino from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7a85-125">**To add Nuclino from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7a85-125">**To add Nuclino from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a85-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b7a85-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b7a85-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b7a85-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="b7a85-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b7a85-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b7a85-133">In the search box, type **Nuclino**, select **Nuclino** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b7a85-133">In the search box, type **Nuclino**, select **Nuclino** from result panel then click **Add** button to add the application.</span></span>

    ![Nuclino in the results list](./media/nuclino-tutorial/tutorial_nuclino_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b7a85-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7a85-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b7a85-136">In this section, you configure and test Azure AD single sign-on with Nuclino based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7a85-136">In this section, you configure and test Azure AD single sign-on with Nuclino based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7a85-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nuclino is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a85-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nuclino is to a user in Azure AD.</span></span> <span data-ttu-id="b7a85-138">In other words, a link relationship between an Azure AD user and the related user in Nuclino needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b7a85-138">In other words, a link relationship between an Azure AD user and the related user in Nuclino needs to be established.</span></span>

<span data-ttu-id="b7a85-139">To configure and test Azure AD single sign-on with Nuclino, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7a85-139">To configure and test Azure AD single sign-on with Nuclino, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7a85-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b7a85-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7a85-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7a85-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7a85-142">**[Create a Nuclino test user](#create-a-nuclino-test-user)** - to have a counterpart of Britta Simon in Nuclino that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b7a85-142">**[Create a Nuclino test user](#create-a-nuclino-test-user)** - to have a counterpart of Britta Simon in Nuclino that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7a85-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b7a85-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7a85-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b7a85-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b7a85-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7a85-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b7a85-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nuclino application.</span><span class="sxs-lookup"><span data-stu-id="b7a85-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nuclino application.</span></span>

<span data-ttu-id="b7a85-147">**To configure Azure AD single sign-on with Nuclino, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7a85-147">**To configure Azure AD single sign-on with Nuclino, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a85-148">In the Azure portal, on the **Nuclino** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-148">In the Azure portal, on the **Nuclino** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="b7a85-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b7a85-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/nuclino-tutorial/tutorial_nuclino_samlbase.png)

3. <span data-ttu-id="b7a85-152">On the **Nuclino Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b7a85-152">On the **Nuclino Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Nuclino Domain and URLs single sign-on information](./media/nuclino-tutorial/tutorial_nuclino_url1.png)

    <span data-ttu-id="b7a85-154">a.</span><span class="sxs-lookup"><span data-stu-id="b7a85-154">a.</span></span> <span data-ttu-id="b7a85-155">In the **Identifier** textbox, type a URL using the following pattern: `https://api.nuclino.com/api/sso/<UNIQUE-ID>/metadata`</span><span class="sxs-lookup"><span data-stu-id="b7a85-155">In the **Identifier** textbox, type a URL using the following pattern: `https://api.nuclino.com/api/sso/<UNIQUE-ID>/metadata`</span></span>

    <span data-ttu-id="b7a85-156">b.</span><span class="sxs-lookup"><span data-stu-id="b7a85-156">b.</span></span> <span data-ttu-id="b7a85-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.nuclino.com/api/sso/<UNIQUE-ID>/acs`</span><span class="sxs-lookup"><span data-stu-id="b7a85-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.nuclino.com/api/sso/<UNIQUE-ID>/acs`</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7a85-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b7a85-158">These values are not real.</span></span> <span data-ttu-id="b7a85-159">Update these values with the actual Identifier and Reply URL from the **Authentication** section, which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b7a85-159">Update these values with the actual Identifier and Reply URL from the **Authentication** section, which is explained later in this tutorial.</span></span>

4. <span data-ttu-id="b7a85-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b7a85-160">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Nuclino Domain and URLs single sign-on information](./media/nuclino-tutorial/tutorial_nuclino_url2.png)

    <span data-ttu-id="b7a85-162">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.nuclino.com/<UNIQUE-ID>/login`</span><span class="sxs-lookup"><span data-stu-id="b7a85-162">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.nuclino.com/<UNIQUE-ID>/login`</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7a85-163">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="b7a85-163">This value is not real.</span></span> <span data-ttu-id="b7a85-164">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="b7a85-164">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b7a85-165">Contact [Nuclino Client support team](mailto:contact@nuclino.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="b7a85-165">Contact [Nuclino Client support team](mailto:contact@nuclino.com) to get this value.</span></span>

5. <span data-ttu-id="b7a85-166">Nuclino application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="b7a85-166">Nuclino application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b7a85-167">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="b7a85-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="b7a85-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="b7a85-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b7a85-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="b7a85-169">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/Nuclino-tutorial/tutorial_attribute.png)

6. <span data-ttu-id="b7a85-171">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="b7a85-171">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="b7a85-172">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="b7a85-172">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="b7a85-173">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="b7a85-173">Attribute Name</span></span> | <span data-ttu-id="b7a85-174">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="b7a85-174">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="b7a85-175">first_name</span><span class="sxs-lookup"><span data-stu-id="b7a85-175">first_name</span></span> | <span data-ttu-id="b7a85-176">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b7a85-176">user.givenname</span></span> |
    | <span data-ttu-id="b7a85-177">last_name</span><span class="sxs-lookup"><span data-stu-id="b7a85-177">last_name</span></span> | <span data-ttu-id="b7a85-178">user.surname</span><span class="sxs-lookup"><span data-stu-id="b7a85-178">user.surname</span></span> |

    <span data-ttu-id="b7a85-179">a.</span><span class="sxs-lookup"><span data-stu-id="b7a85-179">a.</span></span> <span data-ttu-id="b7a85-180">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7a85-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/nuclino-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/nuclino-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b7a85-183">b.</span><span class="sxs-lookup"><span data-stu-id="b7a85-183">b.</span></span> <span data-ttu-id="b7a85-184">In the **Name** textbox, type the **attribute name** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b7a85-184">In the **Name** textbox, type the **attribute name** shown for that row.</span></span>

    <span data-ttu-id="b7a85-185">c.</span><span class="sxs-lookup"><span data-stu-id="b7a85-185">c.</span></span> <span data-ttu-id="b7a85-186">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="b7a85-186">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="b7a85-187">d.</span><span class="sxs-lookup"><span data-stu-id="b7a85-187">d.</span></span> <span data-ttu-id="b7a85-188">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-188">Click **Ok**.</span></span>

7. <span data-ttu-id="b7a85-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b7a85-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/nuclino-tutorial/tutorial_nuclino_certificate.png)

8. <span data-ttu-id="b7a85-191">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b7a85-191">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/nuclino-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="b7a85-193">On the **Nuclino Configuration** section, click **Configure Nuclino** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="b7a85-193">On the **Nuclino Configuration** section, click **Configure Nuclino** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b7a85-194">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="b7a85-194">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Nuclino Configuration](./media/nuclino-tutorial/tutorial_nuclino_configure.png)

10. <span data-ttu-id="b7a85-196">In a different web browser window, sign in to your Nuclino company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b7a85-196">In a different web browser window, sign in to your Nuclino company site as an administrator.</span></span>

11. <span data-ttu-id="b7a85-197">Click on the **ICON**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-197">Click on the **ICON**.</span></span>

    ![Nuclino Configuration](./media/nuclino-tutorial/configure1.png)

12. <span data-ttu-id="b7a85-199">Click on the **Azure AD SSO** and select **Team settings** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="b7a85-199">Click on the **Azure AD SSO** and select **Team settings** from the dropdown.</span></span>

    ![Nuclino Configuration](./media/nuclino-tutorial/configure2.png)

13. <span data-ttu-id="b7a85-201">Select **Authentication** from left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="b7a85-201">Select **Authentication** from left navigation pane.</span></span>

    ![Nuclino Configuration](./media/nuclino-tutorial/configure3.png)

14. <span data-ttu-id="b7a85-203">In the **Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7a85-203">In the **Authentication** section, perform the following steps:</span></span>

    ![Nuclino Configuration](./media/nuclino-tutorial/configure4.png)

    <span data-ttu-id="b7a85-205">a.</span><span class="sxs-lookup"><span data-stu-id="b7a85-205">a.</span></span> <span data-ttu-id="b7a85-206">Select **SAML-based single sign-on (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-206">Select **SAML-based single sign-on (SSO)**.</span></span>

    <span data-ttu-id="b7a85-207">b.</span><span class="sxs-lookup"><span data-stu-id="b7a85-207">b.</span></span> <span data-ttu-id="b7a85-208">Copy **ACS URL (You need to copy and paste this to your SSO provider)** value and paste it into the **Reply URL** textbox of the **Nuclino Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7a85-208">Copy **ACS URL (You need to copy and paste this to your SSO provider)** value and paste it into the **Reply URL** textbox of the **Nuclino Domain and URLs** section in the Azure portal.</span></span>

    <span data-ttu-id="b7a85-209">c.</span><span class="sxs-lookup"><span data-stu-id="b7a85-209">c.</span></span> <span data-ttu-id="b7a85-210">Copy **Entity ID (You need to copy and paste this to your SSO provider)** value and paste it into the **Identifier** textbox of the **Nuclino Domain and URLs** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7a85-210">Copy **Entity ID (You need to copy and paste this to your SSO provider)** value and paste it into the **Identifier** textbox of the **Nuclino Domain and URLs** section in the Azure portal.</span></span>

    <span data-ttu-id="b7a85-211">d.</span><span class="sxs-lookup"><span data-stu-id="b7a85-211">d.</span></span> <span data-ttu-id="b7a85-212">In the **SSO URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7a85-212">In the **SSO URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="b7a85-213">e.</span><span class="sxs-lookup"><span data-stu-id="b7a85-213">e.</span></span> <span data-ttu-id="b7a85-214">In the **Entity ID** textbox, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7a85-214">In the **Entity ID** textbox, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="b7a85-215">f.</span><span class="sxs-lookup"><span data-stu-id="b7a85-215">f.</span></span> <span data-ttu-id="b7a85-216">Open your downloaded **Certificate(Base64)** file in Notepad.</span><span class="sxs-lookup"><span data-stu-id="b7a85-216">Open your downloaded **Certificate(Base64)** file in Notepad.</span></span> <span data-ttu-id="b7a85-217">Copy the content of it into your clipboard, and then paste it to the **Public certificate** text box.</span><span class="sxs-lookup"><span data-stu-id="b7a85-217">Copy the content of it into your clipboard, and then paste it to the **Public certificate** text box.</span></span>

    <span data-ttu-id="b7a85-218">g.</span><span class="sxs-lookup"><span data-stu-id="b7a85-218">g.</span></span> <span data-ttu-id="b7a85-219">Click **SAVE CHANGES**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-219">Click **SAVE CHANGES**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7a85-220">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7a85-220">Create an Azure AD test user</span></span>

<span data-ttu-id="b7a85-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7a85-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b7a85-223">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7a85-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a85-224">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b7a85-224">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/nuclino-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b7a85-226">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-226">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/nuclino-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b7a85-228">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b7a85-228">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/nuclino-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b7a85-230">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7a85-230">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/nuclino-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b7a85-232">a.</span><span class="sxs-lookup"><span data-stu-id="b7a85-232">a.</span></span> <span data-ttu-id="b7a85-233">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-233">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7a85-234">b.</span><span class="sxs-lookup"><span data-stu-id="b7a85-234">b.</span></span> <span data-ttu-id="b7a85-235">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7a85-235">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b7a85-236">c.</span><span class="sxs-lookup"><span data-stu-id="b7a85-236">c.</span></span> <span data-ttu-id="b7a85-237">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b7a85-237">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b7a85-238">d.</span><span class="sxs-lookup"><span data-stu-id="b7a85-238">d.</span></span> <span data-ttu-id="b7a85-239">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-239">Click **Create**.</span></span>

### <a name="create-a-nuclino-test-user"></a><span data-ttu-id="b7a85-240">Create a Nuclino test user</span><span class="sxs-lookup"><span data-stu-id="b7a85-240">Create a Nuclino test user</span></span>

<span data-ttu-id="b7a85-241">The objective of this section is to create a user called Britta Simon in Nuclino.</span><span class="sxs-lookup"><span data-stu-id="b7a85-241">The objective of this section is to create a user called Britta Simon in Nuclino.</span></span> <span data-ttu-id="b7a85-242">Nuclino supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b7a85-242">Nuclino supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b7a85-243">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b7a85-243">There is no action item for you in this section.</span></span> <span data-ttu-id="b7a85-244">A new user is created during an attempt to access Nuclino if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="b7a85-244">A new user is created during an attempt to access Nuclino if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="b7a85-245">If you need to create a user manually, contact [Nuclino support team](mailto:contact@nuclino.com).</span><span class="sxs-lookup"><span data-stu-id="b7a85-245">If you need to create a user manually, contact [Nuclino support team](mailto:contact@nuclino.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b7a85-246">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7a85-246">Assign the Azure AD test user</span></span>

<span data-ttu-id="b7a85-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nuclino.</span><span class="sxs-lookup"><span data-stu-id="b7a85-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nuclino.</span></span>

![Assign the user role][200]

<span data-ttu-id="b7a85-249">**To assign Britta Simon to Nuclino, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7a85-249">**To assign Britta Simon to Nuclino, perform the following steps:**</span></span>

1. <span data-ttu-id="b7a85-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="b7a85-252">In the applications list, select **Nuclino**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-252">In the applications list, select **Nuclino**.</span></span>

    ![The Nuclino link in the Applications list](./media/nuclino-tutorial/tutorial_nuclino_app.png)  

3. <span data-ttu-id="b7a85-254">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b7a85-254">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b7a85-256">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b7a85-256">Click **Add** button.</span></span> <span data-ttu-id="b7a85-257">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7a85-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b7a85-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b7a85-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b7a85-260">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7a85-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7a85-261">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7a85-261">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="b7a85-262">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7a85-262">Test single sign-on</span></span>

<span data-ttu-id="b7a85-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b7a85-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b7a85-264">When you click the Nuclino tile in the Access Panel, you should get automatically signed-on to your Nuclino application.</span><span class="sxs-lookup"><span data-stu-id="b7a85-264">When you click the Nuclino tile in the Access Panel, you should get automatically signed-on to your Nuclino application.</span></span>
<span data-ttu-id="b7a85-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b7a85-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7a85-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b7a85-266">Additional resources</span></span>

* [<span data-ttu-id="b7a85-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7a85-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b7a85-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7a85-268">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/nuclino-tutorial/tutorial_general_01.png
[2]: ./media/nuclino-tutorial/tutorial_general_02.png
[3]: ./media/nuclino-tutorial/tutorial_general_03.png
[4]: ./media/nuclino-tutorial/tutorial_general_04.png

[100]: ./media/nuclino-tutorial/tutorial_general_100.png

[200]: ./media/nuclino-tutorial/tutorial_general_200.png
[201]: ./media/nuclino-tutorial/tutorial_general_201.png
[202]: ./media/nuclino-tutorial/tutorial_general_202.png
[203]: ./media/nuclino-tutorial/tutorial_general_203.png