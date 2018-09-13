---
title: 'Tutorial: Azure Active Directory integration with Comeet Recruiting Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Comeet Recruiting Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 75f51dc9-9525-4ec6-80bf-28374f0c8adf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2018
ms.author: jeedes
ms.openlocfilehash: 137ba7a7e82ff3e57d862868859e8049838701a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866534"
---
# <a name="tutorial-azure-active-directory-integration-with-comeet-recruiting-software"></a><span data-ttu-id="98bb6-103">Tutorial: Azure Active Directory integration with Comeet Recruiting Software</span><span class="sxs-lookup"><span data-stu-id="98bb6-103">Tutorial: Azure Active Directory integration with Comeet Recruiting Software</span></span>

<span data-ttu-id="98bb6-104">In this tutorial, you learn how to integrate Comeet Recruiting Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98bb6-104">In this tutorial, you learn how to integrate Comeet Recruiting Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98bb6-105">Integrating Comeet Recruiting Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="98bb6-105">Integrating Comeet Recruiting Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98bb6-106">You can control in Azure AD who has access to Comeet Recruiting Software.</span><span class="sxs-lookup"><span data-stu-id="98bb6-106">You can control in Azure AD who has access to Comeet Recruiting Software.</span></span>
- <span data-ttu-id="98bb6-107">You can enable your users to automatically get signed-on to Comeet Recruiting Software (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="98bb6-107">You can enable your users to automatically get signed-on to Comeet Recruiting Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="98bb6-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="98bb6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="98bb6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="98bb6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98bb6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98bb6-110">Prerequisites</span></span>

<span data-ttu-id="98bb6-111">To configure Azure AD integration with Comeet Recruiting Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="98bb6-111">To configure Azure AD integration with Comeet Recruiting Software, you need the following items:</span></span>

- <span data-ttu-id="98bb6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="98bb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98bb6-113">A Comeet Recruiting Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="98bb6-113">A Comeet Recruiting Software single sign-on enabled subscription</span></span>

<span data-ttu-id="98bb6-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="98bb6-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98bb6-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98bb6-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98bb6-116">Scenario description</span><span class="sxs-lookup"><span data-stu-id="98bb6-116">Scenario description</span></span>

<span data-ttu-id="98bb6-117">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="98bb6-117">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98bb6-118">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="98bb6-118">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98bb6-119">Adding Comeet Recruiting Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="98bb6-119">Adding Comeet Recruiting Software from the gallery</span></span>
2. <span data-ttu-id="98bb6-120">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98bb6-120">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-comeet-recruiting-software-from-the-gallery"></a><span data-ttu-id="98bb6-121">Adding Comeet Recruiting Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="98bb6-121">Adding Comeet Recruiting Software from the gallery</span></span>

<span data-ttu-id="98bb6-122">To configure the integration of Comeet Recruiting Software into Azure AD, you need to add Comeet Recruiting Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="98bb6-122">To configure the integration of Comeet Recruiting Software into Azure AD, you need to add Comeet Recruiting Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98bb6-123">**To add Comeet Recruiting Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98bb6-123">**To add Comeet Recruiting Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98bb6-124">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="98bb6-124">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="98bb6-126">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-126">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98bb6-127">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-127">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="98bb6-129">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="98bb6-129">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="98bb6-131">In the search box, type **Comeet Recruiting Software**, select **Comeet Recruiting Software** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="98bb6-131">In the search box, type **Comeet Recruiting Software**, select **Comeet Recruiting Software** from result panel then click **Add** button to add the application.</span></span>

    ![Comeet Recruiting Software in the results list](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="98bb6-133">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98bb6-133">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="98bb6-134">In this section, you configure and test Azure AD single sign-on with Comeet Recruiting Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="98bb6-134">In this section, you configure and test Azure AD single sign-on with Comeet Recruiting Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="98bb6-135">For single sign-on to work, Azure AD needs to know what the counterpart user in Comeet Recruiting Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98bb6-135">For single sign-on to work, Azure AD needs to know what the counterpart user in Comeet Recruiting Software is to a user in Azure AD.</span></span> <span data-ttu-id="98bb6-136">In other words, a link relationship between an Azure AD user and the related user in Comeet Recruiting Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="98bb6-136">In other words, a link relationship between an Azure AD user and the related user in Comeet Recruiting Software needs to be established.</span></span>

<span data-ttu-id="98bb6-137">To configure and test Azure AD single sign-on with Comeet Recruiting Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="98bb6-137">To configure and test Azure AD single sign-on with Comeet Recruiting Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98bb6-138">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="98bb6-138">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="98bb6-139">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98bb6-139">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98bb6-140">**[Create a Comeet Recruiting Software test user](#create-a-comeet-recruiting-software-test-user)** - to have a counterpart of Britta Simon in Comeet Recruiting Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="98bb6-140">**[Create a Comeet Recruiting Software test user](#create-a-comeet-recruiting-software-test-user)** - to have a counterpart of Britta Simon in Comeet Recruiting Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="98bb6-141">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="98bb6-141">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98bb6-142">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="98bb6-142">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="98bb6-143">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="98bb6-143">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="98bb6-144">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Comeet Recruiting Software application.</span><span class="sxs-lookup"><span data-stu-id="98bb6-144">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Comeet Recruiting Software application.</span></span>

<span data-ttu-id="98bb6-145">**To configure Azure AD single sign-on with Comeet Recruiting Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98bb6-145">**To configure Azure AD single sign-on with Comeet Recruiting Software, perform the following steps:**</span></span>

1. <span data-ttu-id="98bb6-146">In the Azure portal, on the **Comeet Recruiting Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-146">In the Azure portal, on the **Comeet Recruiting Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="98bb6-148">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="98bb6-148">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_samlbase.png)

3. <span data-ttu-id="98bb6-150">On the **Comeet Recruiting Software Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="98bb6-150">On the **Comeet Recruiting Software Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Comeet Domain and URLs single sign-on information](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_url1.png)

    <span data-ttu-id="98bb6-152">a.</span><span class="sxs-lookup"><span data-stu-id="98bb6-152">a.</span></span> <span data-ttu-id="98bb6-153">In the **Identifier** textbox, type a URL using the following pattern: `https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/`</span><span class="sxs-lookup"><span data-stu-id="98bb6-153">In the **Identifier** textbox, type a URL using the following pattern: `https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/`</span></span>

    <span data-ttu-id="98bb6-154">b.</span><span class="sxs-lookup"><span data-stu-id="98bb6-154">b.</span></span> <span data-ttu-id="98bb6-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/`</span><span class="sxs-lookup"><span data-stu-id="98bb6-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/`</span></span>

    > [!NOTE]
    > <span data-ttu-id="98bb6-156">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="98bb6-156">These values are not real.</span></span> <span data-ttu-id="98bb6-157">Update these values with the actual Identifier, Reply URL.</span><span class="sxs-lookup"><span data-stu-id="98bb6-157">Update these values with the actual Identifier, Reply URL.</span></span> <span data-ttu-id="98bb6-158">You will get these values from the Comeet Recruiting Software portal as shown in the [support page](https://support.comeet.co/knowledgebase/adfs-single-sign-on/).</span><span class="sxs-lookup"><span data-stu-id="98bb6-158">You will get these values from the Comeet Recruiting Software portal as shown in the [support page](https://support.comeet.co/knowledgebase/adfs-single-sign-on/).</span></span>

4. <span data-ttu-id="98bb6-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="98bb6-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Comeet Recruiting Software Domain and URLs single sign-on information](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_url2.png)

    <span data-ttu-id="98bb6-161">In the **Sign-on URL** textbox, type the URL: `https://app.comeet.co`</span><span class="sxs-lookup"><span data-stu-id="98bb6-161">In the **Sign-on URL** textbox, type the URL: `https://app.comeet.co`</span></span>

5. <span data-ttu-id="98bb6-162">Comeet Recruiting Software application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="98bb6-162">Comeet Recruiting Software application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="98bb6-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="98bb6-163">The following screenshot shows an example for this.</span></span> <span data-ttu-id="98bb6-164">The default value of **User Identifier** is **user.userprincipalname** but **Comeet Recruiting Software** expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="98bb6-164">The default value of **User Identifier** is **user.userprincipalname** but **Comeet Recruiting Software** expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="98bb6-165">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="98bb6-165">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span>

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_attribute.png)

6. <span data-ttu-id="98bb6-167">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="98bb6-167">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="98bb6-168">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="98bb6-168">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="98bb6-169">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="98bb6-169">Attribute Name</span></span> | <span data-ttu-id="98bb6-170">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="98bb6-170">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="98bb6-171">comeet_id</span><span class="sxs-lookup"><span data-stu-id="98bb6-171">comeet_id</span></span> | <span data-ttu-id="98bb6-172">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="98bb6-172">user.userprincipalname</span></span> |

    <span data-ttu-id="98bb6-173">a.</span><span class="sxs-lookup"><span data-stu-id="98bb6-173">a.</span></span> <span data-ttu-id="98bb6-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="98bb6-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="98bb6-177">b.</span><span class="sxs-lookup"><span data-stu-id="98bb6-177">b.</span></span> <span data-ttu-id="98bb6-178">In the **Name** textbox, type the **attribute name** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="98bb6-178">In the **Name** textbox, type the **attribute name** shown for that row.</span></span>

    <span data-ttu-id="98bb6-179">c.</span><span class="sxs-lookup"><span data-stu-id="98bb6-179">c.</span></span> <span data-ttu-id="98bb6-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="98bb6-180">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="98bb6-181">d.</span><span class="sxs-lookup"><span data-stu-id="98bb6-181">d.</span></span> <span data-ttu-id="98bb6-182">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-182">Click **Ok**.</span></span>

7. <span data-ttu-id="98bb6-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="98bb6-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_certificate.png)

8. <span data-ttu-id="98bb6-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="98bb6-185">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/comeetrecruitingsoftware-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="98bb6-187">To configure single sign-on on **Comeet Recruiting Software** side, paste the content of the downloaded Metadata XML into Comeet Recruiting Software, as shown in the [Support Page](https://support.comeet.co/knowledgebase/adfs-single-sign-on/).</span><span class="sxs-lookup"><span data-stu-id="98bb6-187">To configure single sign-on on **Comeet Recruiting Software** side, paste the content of the downloaded Metadata XML into Comeet Recruiting Software, as shown in the [Support Page](https://support.comeet.co/knowledgebase/adfs-single-sign-on/).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="98bb6-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="98bb6-188">Create an Azure AD test user</span></span>

<span data-ttu-id="98bb6-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98bb6-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="98bb6-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98bb6-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98bb6-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="98bb6-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/comeetrecruitingsoftware-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="98bb6-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/comeetrecruitingsoftware-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="98bb6-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="98bb6-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/comeetrecruitingsoftware-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="98bb6-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="98bb6-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/comeetrecruitingsoftware-tutorial/create_aaduser_04.png)

    <span data-ttu-id="98bb6-200">a.</span><span class="sxs-lookup"><span data-stu-id="98bb6-200">a.</span></span> <span data-ttu-id="98bb6-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98bb6-202">b.</span><span class="sxs-lookup"><span data-stu-id="98bb6-202">b.</span></span> <span data-ttu-id="98bb6-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98bb6-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="98bb6-204">c.</span><span class="sxs-lookup"><span data-stu-id="98bb6-204">c.</span></span> <span data-ttu-id="98bb6-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="98bb6-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="98bb6-206">d.</span><span class="sxs-lookup"><span data-stu-id="98bb6-206">d.</span></span> <span data-ttu-id="98bb6-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-207">Click **Create**.</span></span>

### <a name="create-a-comeet-recruiting-software-test-user"></a><span data-ttu-id="98bb6-208">Create a Comeet Recruiting Software test user</span><span class="sxs-lookup"><span data-stu-id="98bb6-208">Create a Comeet Recruiting Software test user</span></span>

<span data-ttu-id="98bb6-209">In this section, you create a user called Britta Simon in Comeet Recruiting Software.</span><span class="sxs-lookup"><span data-stu-id="98bb6-209">In this section, you create a user called Britta Simon in Comeet Recruiting Software.</span></span> <span data-ttu-id="98bb6-210">Work with [Comeet Recruiting Software support team](mailto:support@comeet.co) to add the users in the Comeet Recruiting Software platform.</span><span class="sxs-lookup"><span data-stu-id="98bb6-210">Work with [Comeet Recruiting Software support team](mailto:support@comeet.co) to add the users in the Comeet Recruiting Software platform.</span></span> <span data-ttu-id="98bb6-211">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="98bb6-211">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="98bb6-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="98bb6-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="98bb6-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Comeet Recruiting Software.</span><span class="sxs-lookup"><span data-stu-id="98bb6-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Comeet Recruiting Software.</span></span>

![Assign the user role][200]

<span data-ttu-id="98bb6-215">**To assign Britta Simon to Comeet Recruiting Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="98bb6-215">**To assign Britta Simon to Comeet Recruiting Software, perform the following steps:**</span></span>

1. <span data-ttu-id="98bb6-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="98bb6-218">In the applications list, select **Comeet Recruiting Software**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-218">In the applications list, select **Comeet Recruiting Software**.</span></span>

    ![The Comeet Recruiting Software link in the Applications list](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_app.png)  

3. <span data-ttu-id="98bb6-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="98bb6-220">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="98bb6-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="98bb6-222">Click **Add** button.</span></span> <span data-ttu-id="98bb6-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="98bb6-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="98bb6-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="98bb6-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="98bb6-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="98bb6-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98bb6-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="98bb6-227">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="98bb6-228">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="98bb6-228">Test single sign-on</span></span>

<span data-ttu-id="98bb6-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="98bb6-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="98bb6-230">When you click the Comeet Recruiting Software tile in the Access Panel, you should get automatically signed-on to your Comeet Recruiting Software application.</span><span class="sxs-lookup"><span data-stu-id="98bb6-230">When you click the Comeet Recruiting Software tile in the Access Panel, you should get automatically signed-on to your Comeet Recruiting Software application.</span></span>
<span data-ttu-id="98bb6-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98bb6-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98bb6-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="98bb6-232">Additional resources</span></span>

* [<span data-ttu-id="98bb6-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98bb6-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="98bb6-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98bb6-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_01.png
[2]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_02.png
[3]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_03.png
[4]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_04.png

[100]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_100.png

[200]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_200.png
[201]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_201.png
[202]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_202.png
[203]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_203.png