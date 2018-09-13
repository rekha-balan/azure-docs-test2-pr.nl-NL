---
title: 'Tutorial: Azure Active Directory integration with ProMaster (by Inlogik) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ProMaster (by Inlogik).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 348dbd37-dc4f-49df-bb90-53d249d456b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2018
ms.author: jeedes
ms.openlocfilehash: 13bb128836590fb43e0c6a2f7131f83a99a23eaf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865421"
---
# <a name="tutorial-azure-active-directory-integration-with-promaster-by-inlogik"></a><span data-ttu-id="a5f0b-103">Tutorial: Azure Active Directory integration with ProMaster (by Inlogik)</span><span class="sxs-lookup"><span data-stu-id="a5f0b-103">Tutorial: Azure Active Directory integration with ProMaster (by Inlogik)</span></span>

<span data-ttu-id="a5f0b-104">In this tutorial, you learn how to integrate ProMaster (by Inlogik) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-104">In this tutorial, you learn how to integrate ProMaster (by Inlogik) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5f0b-105">Integrating ProMaster (by Inlogik) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-105">Integrating ProMaster (by Inlogik) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5f0b-106">You can control in Azure AD who has access to ProMaster (by Inlogik).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-106">You can control in Azure AD who has access to ProMaster (by Inlogik).</span></span>
- <span data-ttu-id="a5f0b-107">You can enable your users to automatically get signed-on to ProMaster (by Inlogik) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-107">You can enable your users to automatically get signed-on to ProMaster (by Inlogik) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a5f0b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a5f0b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="a5f0b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5f0b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5f0b-110">Prerequisites</span></span>

<span data-ttu-id="a5f0b-111">To configure Azure AD integration with ProMaster (by Inlogik), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-111">To configure Azure AD integration with ProMaster (by Inlogik), you need the following items:</span></span>

- <span data-ttu-id="a5f0b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a5f0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5f0b-113">A ProMaster (by Inlogik) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a5f0b-113">A ProMaster (by Inlogik) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5f0b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5f0b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5f0b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5f0b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5f0b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a5f0b-118">Scenario description</span></span>

<span data-ttu-id="a5f0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="a5f0b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5f0b-121">Adding ProMaster (by Inlogik) from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5f0b-121">Adding ProMaster (by Inlogik) from the gallery</span></span>
2. <span data-ttu-id="a5f0b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5f0b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promaster-by-inlogik-from-the-gallery"></a><span data-ttu-id="a5f0b-123">Adding ProMaster (by Inlogik) from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5f0b-123">Adding ProMaster (by Inlogik) from the gallery</span></span>

<span data-ttu-id="a5f0b-124">To configure the integration of ProMaster (by Inlogik) into Azure AD, you need to add ProMaster (by Inlogik) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-124">To configure the integration of ProMaster (by Inlogik) into Azure AD, you need to add ProMaster (by Inlogik) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5f0b-125">**To add ProMaster (by Inlogik) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5f0b-125">**To add ProMaster (by Inlogik) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5f0b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="a5f0b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5f0b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="a5f0b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="a5f0b-133">In the search box, type **ProMaster (by Inlogik)**, select **ProMaster (by Inlogik)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-133">In the search box, type **ProMaster (by Inlogik)**, select **ProMaster (by Inlogik)** from result panel then click **Add** button to add the application.</span></span>

    ![ProMaster (by Inlogik) in the results list](./media/promaster-tutorial/tutorial_promaster_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a5f0b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5f0b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a5f0b-136">In this section, you configure and test Azure AD single sign-on with ProMaster (by Inlogik) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a5f0b-136">In this section, you configure and test Azure AD single sign-on with ProMaster (by Inlogik) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5f0b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ProMaster (by Inlogik) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ProMaster (by Inlogik) is to a user in Azure AD.</span></span> <span data-ttu-id="a5f0b-138">In other words, a link relationship between an Azure AD user and the related user in ProMaster (by Inlogik) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-138">In other words, a link relationship between an Azure AD user and the related user in ProMaster (by Inlogik) needs to be established.</span></span>

<span data-ttu-id="a5f0b-139">To configure and test Azure AD single sign-on with ProMaster (by Inlogik), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-139">To configure and test Azure AD single sign-on with ProMaster (by Inlogik), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5f0b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5f0b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5f0b-142">**[Create a ProMaster (by Inlogik) test user](#create-a-promaster-by-inlogik-test-user)** - to have a counterpart of Britta Simon in ProMaster (by Inlogik) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-142">**[Create a ProMaster (by Inlogik) test user](#create-a-promaster-by-inlogik-test-user)** - to have a counterpart of Britta Simon in ProMaster (by Inlogik) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5f0b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5f0b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a5f0b-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5f0b-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a5f0b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ProMaster (by Inlogik) application.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ProMaster (by Inlogik) application.</span></span>

<span data-ttu-id="a5f0b-147">**To configure Azure AD single sign-on with ProMaster (by Inlogik), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5f0b-147">**To configure Azure AD single sign-on with ProMaster (by Inlogik), perform the following steps:**</span></span>

1. <span data-ttu-id="a5f0b-148">In the Azure portal, on the **ProMaster (by Inlogik)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-148">In the Azure portal, on the **ProMaster (by Inlogik)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="a5f0b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/promaster-tutorial/tutorial_promaster_samlbase.png)

3. <span data-ttu-id="a5f0b-152">On the **ProMaster (by Inlogik) Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-152">On the **ProMaster (by Inlogik) Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![ProMaster (by Inlogik) Domain and URLs single sign-on information](./media/promaster-tutorial/tutorial_promaster_url1.png)

    <span data-ttu-id="a5f0b-154">a.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-154">a.</span></span> <span data-ttu-id="a5f0b-155">In the **Identifier** textbox, use one of the following URL pattern:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-155">In the **Identifier** textbox, use one of the following URL pattern:</span></span>
    | |
    | - |-|
    |  `https://secure.inlogik.com/<COMPANYNAME>`|
    | `https://<CUSTOMDOMAIN>/SAMLBASE`|
    | |

    <span data-ttu-id="a5f0b-156">b.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-156">b.</span></span> <span data-ttu-id="a5f0b-157">In the **Reply URL** textbox, use one of the following URL pattern:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-157">In the **Reply URL** textbox, use one of the following URL pattern:</span></span>
    | |
    | - |-|
    | `https://secure.inlogik.com/<COMPANYNAME>/saml/acs`|
    | `https://<CUSTOMDOMAIN>/SAMLBASE/saml/acs`|
    | |

4. <span data-ttu-id="a5f0b-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ProMaster (by Inlogik) Domain and URLs single sign-on information](./media/promaster-tutorial/tutorial_promaster_url2.png)

    <span data-ttu-id="a5f0b-160">In the **Sign-on URL** textbox, use one of the following URL pattern:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-160">In the **Sign-on URL** textbox, use one of the following URL pattern:</span></span>
    | |
    | - |-|
    | `https://secure.inlogik.com/<COMPANYNAME>/saml/acs `|
    | `https://<CUSTOMDOMAIN>/SAMLBASE/saml/acs`|
    | |

    > [!NOTE]
    > <span data-ttu-id="a5f0b-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-161">These values are not real.</span></span> <span data-ttu-id="a5f0b-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a5f0b-163">Contact [ProMaster (by Inlogik) Client support team](mailto:michael.boldiston@inlogik.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-163">Contact [ProMaster (by Inlogik) Client support team](mailto:michael.boldiston@inlogik.com) to get these values.</span></span>

5. <span data-ttu-id="a5f0b-164">On the **SAML Signing Certificate** section, click the co button to copy **App Federation Metadata Url** and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-164">On the **SAML Signing Certificate** section, click the co button to copy **App Federation Metadata Url** and paste it into Notepad.</span></span>

    ![The Certificate download link](./media/promaster-tutorial/tutorial_promaster_certificate.png)

6. <span data-ttu-id="a5f0b-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/promaster-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a5f0b-168">To configure single sign-on on **ProMaster (by Inlogik)** side, you need to send the **App Federation Metadata Url** to [ProMaster (by Inlogik) support team](mailto:michael.boldiston@inlogik.com).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-168">To configure single sign-on on **ProMaster (by Inlogik)** side, you need to send the **App Federation Metadata Url** to [ProMaster (by Inlogik) support team](mailto:michael.boldiston@inlogik.com).</span></span> <span data-ttu-id="a5f0b-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a5f0b-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5f0b-170">Create an Azure AD test user</span></span>

<span data-ttu-id="a5f0b-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a5f0b-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5f0b-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5f0b-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/promaster-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a5f0b-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/promaster-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a5f0b-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/promaster-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a5f0b-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5f0b-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/promaster-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a5f0b-182">a.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-182">a.</span></span> <span data-ttu-id="a5f0b-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5f0b-184">b.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-184">b.</span></span> <span data-ttu-id="a5f0b-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a5f0b-186">c.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-186">c.</span></span> <span data-ttu-id="a5f0b-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a5f0b-188">d.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-188">d.</span></span> <span data-ttu-id="a5f0b-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-189">Click **Create**.</span></span>

### <a name="create-a-promaster-by-inlogik-test-user"></a><span data-ttu-id="a5f0b-190">Create a ProMaster (by Inlogik) test user</span><span class="sxs-lookup"><span data-stu-id="a5f0b-190">Create a ProMaster (by Inlogik) test user</span></span>

<span data-ttu-id="a5f0b-191">In this section, you create a user called Britta Simon in ProMaster (by Inlogik).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-191">In this section, you create a user called Britta Simon in ProMaster (by Inlogik).</span></span> <span data-ttu-id="a5f0b-192">Work with [ProMaster (by Inlogik) support team](mailto:michael.boldiston@inlogik.com) to add the users in the ProMaster (by Inlogik) platform.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-192">Work with [ProMaster (by Inlogik) support team](mailto:michael.boldiston@inlogik.com) to add the users in the ProMaster (by Inlogik) platform.</span></span> <span data-ttu-id="a5f0b-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a5f0b-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5f0b-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="a5f0b-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ProMaster (by Inlogik).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ProMaster (by Inlogik).</span></span>

![Assign the user role][200]

<span data-ttu-id="a5f0b-197">**To assign Britta Simon to ProMaster (by Inlogik), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5f0b-197">**To assign Britta Simon to ProMaster (by Inlogik), perform the following steps:**</span></span>

1. <span data-ttu-id="a5f0b-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a5f0b-200">In the applications list, select **ProMaster (by Inlogik)**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-200">In the applications list, select **ProMaster (by Inlogik)**.</span></span>

    ![The ProMaster (by Inlogik) link in the Applications list](./media/promaster-tutorial/tutorial_promaster_app.png)  

3. <span data-ttu-id="a5f0b-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="a5f0b-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-204">Click **Add** button.</span></span> <span data-ttu-id="a5f0b-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="a5f0b-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5f0b-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5f0b-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-209">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="a5f0b-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5f0b-210">Test single sign-on</span></span>

<span data-ttu-id="a5f0b-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5f0b-212">When you click the ProMaster (by Inlogik) tile in the Access Panel, you should get automatically signed-on to your ProMaster (by Inlogik) application.</span><span class="sxs-lookup"><span data-stu-id="a5f0b-212">When you click the ProMaster (by Inlogik) tile in the Access Panel, you should get automatically signed-on to your ProMaster (by Inlogik) application.</span></span>
<span data-ttu-id="a5f0b-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5f0b-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5f0b-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a5f0b-214">Additional resources</span></span>

* [<span data-ttu-id="a5f0b-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5f0b-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a5f0b-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5f0b-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/promaster-tutorial/tutorial_general_01.png
[2]: ./media/promaster-tutorial/tutorial_general_02.png
[3]: ./media/promaster-tutorial/tutorial_general_03.png
[4]: ./media/promaster-tutorial/tutorial_general_04.png

[100]: ./media/promaster-tutorial/tutorial_general_100.png

[200]: ./media/promaster-tutorial/tutorial_general_200.png
[201]: ./media/promaster-tutorial/tutorial_general_201.png
[202]: ./media/promaster-tutorial/tutorial_general_202.png
[203]: ./media/promaster-tutorial/tutorial_general_203.png

