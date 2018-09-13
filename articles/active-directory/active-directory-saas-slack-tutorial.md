---
title: 'Tutorial: Azure Active Directory integration with Slack | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Slack.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: cd83ddeabcb7ce01a6e7ad97a4373c400b236acd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563440"
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="95f7e-103">Tutorial: Azure Active Directory integration with Slack</span><span class="sxs-lookup"><span data-stu-id="95f7e-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="95f7e-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95f7e-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95f7e-105">When you integrate Slack with Azure AD, you can:</span><span class="sxs-lookup"><span data-stu-id="95f7e-105">When you integrate Slack with Azure AD, you can:</span></span>

* <span data-ttu-id="95f7e-106">Control in Azure AD who has access to Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-106">Control in Azure AD who has access to Slack.</span></span>
* <span data-ttu-id="95f7e-107">Enable users to sign in automatically to Slack with single sign-on (SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="95f7e-107">Enable users to sign in automatically to Slack with single sign-on (SSO) with their Azure AD accounts.</span></span>
* <span data-ttu-id="95f7e-108">Manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="95f7e-108">Manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="95f7e-109">To learn about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95f7e-109">To learn about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95f7e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="95f7e-110">Prerequisites</span></span>

<span data-ttu-id="95f7e-111">To configure Azure AD integration with Slack, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="95f7e-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

* <span data-ttu-id="95f7e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="95f7e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="95f7e-113">A Slack SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="95f7e-113">A Slack SSO-enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="95f7e-114">We do not recommend testing the steps in this tutorial using a production environment.</span><span class="sxs-lookup"><span data-stu-id="95f7e-114">We do not recommend testing the steps in this tutorial using a production environment.</span></span>
>
>

<span data-ttu-id="95f7e-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="95f7e-115">To test the steps in this tutorial, follow these recommendations:</span></span>

* <span data-ttu-id="95f7e-116">Use your production environment only if necessary.</span><span class="sxs-lookup"><span data-stu-id="95f7e-116">Use your production environment only if necessary.</span></span>
* <span data-ttu-id="95f7e-117">If you don't have an Azure AD trial environment, get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95f7e-117">If you don't have an Azure AD trial environment, get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="95f7e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="95f7e-118">Scenario description</span></span>
<span data-ttu-id="95f7e-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="95f7e-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="95f7e-120">The scenario to be followed consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="95f7e-120">The scenario to be followed consists of two main building blocks:</span></span>

* <span data-ttu-id="95f7e-121">Adding Slack from the gallery</span><span class="sxs-lookup"><span data-stu-id="95f7e-121">Adding Slack from the gallery</span></span>
* <span data-ttu-id="95f7e-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="95f7e-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-slack-from-the-gallery"></a><span data-ttu-id="95f7e-123">Add Slack from the gallery</span><span class="sxs-lookup"><span data-stu-id="95f7e-123">Add Slack from the gallery</span></span>
<span data-ttu-id="95f7e-124">To configure the integration of Slack with Azure AD, add Slack from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="95f7e-124">To configure the integration of Slack with Azure AD, add Slack from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="95f7e-125">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95f7e-125">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="95f7e-126">In the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="95f7e-126">In the left pane, click the **Azure Active Directory** button.</span></span>

    ![The "Azure Active Directory" button][1]

3. <span data-ttu-id="95f7e-128">Go to **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-128">Go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![The "All applications" button on the "Enterprise applications" blade][2]

4. <span data-ttu-id="95f7e-130">At the top of the **All applications** dialog box, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-130">At the top of the **All applications** dialog box, click **Add**.</span></span>

    ![The "Add" button in the "All applications" dialog box][3]

5. <span data-ttu-id="95f7e-132">In the search box, type **Slack**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-132">In the search box, type **Slack**.</span></span>

    ![The "Add an application" search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_000.png)

6. <span data-ttu-id="95f7e-134">In the results pane, select **Slack**, and then click the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="95f7e-134">In the results pane, select **Slack**, and then click the **Add** button to add the application.</span></span>

    ![Select "Slack" in the results pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="95f7e-136">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="95f7e-136">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="95f7e-137">In this section, you configure and test Azure AD SSO with Slack by using the test user "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="95f7e-137">In this section, you configure and test Azure AD SSO with Slack by using the test user "Britta Simon."</span></span>

<span data-ttu-id="95f7e-138">For SSO to work, Azure AD must establish a link relationship between the Azure AD user and its counterpart user in Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-138">For SSO to work, Azure AD must establish a link relationship between the Azure AD user and its counterpart user in Slack.</span></span> <span data-ttu-id="95f7e-139">You establish this link relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-139">You establish this link relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Slack.</span></span>

<span data-ttu-id="95f7e-140">To configure and test Azure AD SSO with Slack, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="95f7e-140">To configure and test Azure AD SSO with Slack, complete the following building blocks:</span></span>

1. <span data-ttu-id="95f7e-141">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable the user to use this feature.</span><span class="sxs-lookup"><span data-stu-id="95f7e-141">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on) to enable the user to use this feature.</span></span>
2. <span data-ttu-id="95f7e-142">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD SSO with user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95f7e-142">[Create an Azure AD test user](#creating-an-azure-ad-test-user) to test Azure AD SSO with user Britta Simon.</span></span>
3. <span data-ttu-id="95f7e-143">[Create a Slack test user](#creating-a-slack-test-user) to give Azure AD user Britta Simon a Slack counterpart to link to.</span><span class="sxs-lookup"><span data-stu-id="95f7e-143">[Create a Slack test user](#creating-a-slack-test-user) to give Azure AD user Britta Simon a Slack counterpart to link to.</span></span>
4. <span data-ttu-id="95f7e-144">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable user Britta Simon to use Azure AD SSO.</span><span class="sxs-lookup"><span data-stu-id="95f7e-144">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user) to enable user Britta Simon to use Azure AD SSO.</span></span>
5. <span data-ttu-id="95f7e-145">[Test single sign-on](#testing-single-sign-on) to verify that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="95f7e-145">[Test single sign-on](#testing-single-sign-on) to verify that the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="95f7e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="95f7e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="95f7e-147">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your Slack application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="95f7e-147">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your Slack application by doing the following:</span></span>

1. <span data-ttu-id="95f7e-148">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-148">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![The Slack application integration page][4]

2. <span data-ttu-id="95f7e-150">In the **Single sign-on** dialog box, in the **Mode** list, select **SAML-based Sign-on** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="95f7e-150">In the **Single sign-on** dialog box, in the **Mode** list, select **SAML-based Sign-on** to enable SSO.</span></span>

    ![The "Single sign-on" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_01.png)

3. <span data-ttu-id="95f7e-152">Under **Slack Domain and URLs**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="95f7e-152">Under **Slack Domain and URLs**, perform the following steps:</span></span>

    ![The "Single sign-on" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_02.png)
  1. <span data-ttu-id="95f7e-154">In the **Sign on URL** box, type a URL that uses the naming convention _https://<company name>.slack.com_.</span><span class="sxs-lookup"><span data-stu-id="95f7e-154">In the **Sign on URL** box, type a URL that uses the naming convention _https://<company name>.slack.com_.</span></span>
  2. <span data-ttu-id="95f7e-155">In the **Identifier** box, type **https://slack.com**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-155">In the **Identifier** box, type **https://slack.com**.</span></span>

     >[!NOTE]
     ><span data-ttu-id="95f7e-156">The preceding values are not real values.</span><span class="sxs-lookup"><span data-stu-id="95f7e-156">The preceding values are not real values.</span></span> <span data-ttu-id="95f7e-157">Here we recommend that you use unique values for the URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="95f7e-157">Here we recommend that you use unique values for the URL and identifier.</span></span> <span data-ttu-id="95f7e-158">Later, you will update the values with the actual URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="95f7e-158">Later, you will update the values with the actual URL and identifier.</span></span> <span data-ttu-id="95f7e-159">To obtain the values, contact the [Slack support team](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="95f7e-159">To obtain the values, contact the [Slack support team](https://slack.com/help/contact).</span></span>
     >
     >

4. <span data-ttu-id="95f7e-160">The Slack application expects the Security Assertion Markup Language (SAML) assertions to be displayed in a specific format.</span><span class="sxs-lookup"><span data-stu-id="95f7e-160">The Slack application expects the Security Assertion Markup Language (SAML) assertions to be displayed in a specific format.</span></span> <span data-ttu-id="95f7e-161">Configure the claims and manage the values of the attributes in the **User Attributes** section of the Slack application integration page, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="95f7e-161">Configure the claims and manage the values of the attributes in the **User Attributes** section of the Slack application integration page, as shown in the following screenshot:</span></span>

    ![Configure claims in the User Attributes section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_03.png)

5. <span data-ttu-id="95f7e-163">In the **Single sign-on** dialog box, in the **User Attributes** section, select **user.mail** as **User Identifier**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-163">In the **Single sign-on** dialog box, in the **User Attributes** section, select **user.mail** as **User Identifier**.</span></span> <span data-ttu-id="95f7e-164">For each row in the table, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="95f7e-164">For each row in the table, perform the following steps:</span></span>

    | <span data-ttu-id="95f7e-165">Attribute name</span><span class="sxs-lookup"><span data-stu-id="95f7e-165">Attribute name</span></span> | <span data-ttu-id="95f7e-166">Attribute value</span><span class="sxs-lookup"><span data-stu-id="95f7e-166">Attribute value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="95f7e-167">User.Email</span><span class="sxs-lookup"><span data-stu-id="95f7e-167">User.Email</span></span> | <span data-ttu-id="95f7e-168">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="95f7e-168">user.userprincipalname</span></span> |
    | <span data-ttu-id="95f7e-169">first_name</span><span class="sxs-lookup"><span data-stu-id="95f7e-169">first_name</span></span> | <span data-ttu-id="95f7e-170">user.givenname</span><span class="sxs-lookup"><span data-stu-id="95f7e-170">user.givenname</span></span> |
    | <span data-ttu-id="95f7e-171">last_name</span><span class="sxs-lookup"><span data-stu-id="95f7e-171">last_name</span></span> | <span data-ttu-id="95f7e-172">user.surname</span><span class="sxs-lookup"><span data-stu-id="95f7e-172">user.surname</span></span> |
    | <span data-ttu-id="95f7e-173">User.Username</span><span class="sxs-lookup"><span data-stu-id="95f7e-173">User.Username</span></span> | <span data-ttu-id="95f7e-174">extractmailprefix([userprincipalname])</span><span class="sxs-lookup"><span data-stu-id="95f7e-174">extractmailprefix([userprincipalname])</span></span> |

    1. <span data-ttu-id="95f7e-175">Click the **Add attribute** button.</span><span class="sxs-lookup"><span data-stu-id="95f7e-175">Click the **Add attribute** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_04.png)
    2. <span data-ttu-id="95f7e-177">In the **Add Attribute** dialog box, in the **Name** box, enter the first name from the table's **Attribute name** column.</span><span class="sxs-lookup"><span data-stu-id="95f7e-177">In the **Add Attribute** dialog box, in the **Name** box, enter the first name from the table's **Attribute name** column.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_05.png)
    3. <span data-ttu-id="95f7e-179">In the **Value** box, enter the first value from the table's **Attribute value** column.</span><span class="sxs-lookup"><span data-stu-id="95f7e-179">In the **Value** box, enter the first value from the table's **Attribute value** column.</span></span>
    4. <span data-ttu-id="95f7e-180">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-180">Click **OK**.</span></span>
    5. <span data-ttu-id="95f7e-181">Repeat steps "a" through "d" for the next three table rows.</span><span class="sxs-lookup"><span data-stu-id="95f7e-181">Repeat steps "a" through "d" for the next three table rows.</span></span>

6. <span data-ttu-id="95f7e-182">Under **SAML Signing Certificate**, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-182">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

    ![Create a certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_06.png)    

7. <span data-ttu-id="95f7e-184">In the **Create New Certificate** dialog box, click the **Calendar** button, select an expiration (expiry) date, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-184">In the **Create New Certificate** dialog box, click the **Calendar** button, select an expiration (expiry) date, and then click **Save**.</span></span>

    ![Select a certificate expiration date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_300.png)

8. <span data-ttu-id="95f7e-186">Under **SAML Signing Certificate**, select the **Make new certificate active** check box, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-186">Under **SAML Signing Certificate**, select the **Make new certificate active** check box, and then click **Save**.</span></span>

    ![Activate the SAML signing certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_07.png)

9. <span data-ttu-id="95f7e-188">In the **Rollover certificate** pop-up window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-188">In the **Rollover certificate** pop-up window, click **OK**.</span></span>

    ![The Rollover certificate pop-up window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="95f7e-190">Under **SAML Signing Certificate**, click **Certificate (base64)**, and then save the certificate file to your local drive.</span><span class="sxs-lookup"><span data-stu-id="95f7e-190">Under **SAML Signing Certificate**, click **Certificate (base64)**, and then save the certificate file to your local drive.</span></span>

    ![Save the certificate to your local drive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_08.png)

11. <span data-ttu-id="95f7e-192">Under **Slack Configuration**, click **Configure Slack** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="95f7e-192">Under **Slack Configuration**, click **Configure Slack** to open the **Configure sign-on** window.</span></span>

    ![Click "Configure Slack" to open the Configure sign-on window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_09.png)

    ![The "Configure sign-on" window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_10.png)

12. <span data-ttu-id="95f7e-195">Open a new browser window, and then sign in to your Slack company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="95f7e-195">Open a new browser window, and then sign in to your Slack company site as an administrator.</span></span>

13. <span data-ttu-id="95f7e-196">Go to **Microsoft Azure AD**, and then go to **Team Settings**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-196">Go to **Microsoft Azure AD**, and then go to **Team Settings**.</span></span>

    ![The Microsoft Azure AD "Team Settings" button on the Slack company site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

14. <span data-ttu-id="95f7e-198">Under **Team Settings**, click the **Authentication** tab, and then click **Change Settings**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-198">Under **Team Settings**, click the **Authentication** tab, and then click **Change Settings**.</span></span>

    ![The "Change Settings" button on the Team Settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

15. <span data-ttu-id="95f7e-200">In the **SAML Authentication Settings** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="95f7e-200">In the **SAML Authentication Settings** dialog box, perform the following steps:</span></span>

    ![The "SAML Authentication Settings" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)
  1. <span data-ttu-id="95f7e-202">In the **SAML 2.0 Endpoint (HTTP)** box, enter the **SAML Single Sign-On Service URL** value from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="95f7e-202">In the **SAML 2.0 Endpoint (HTTP)** box, enter the **SAML Single Sign-On Service URL** value from the Azure AD application configuration window.</span></span>
  2. <span data-ttu-id="95f7e-203">In the **Identity Provider Issuer** box, enter the **SAML Entity ID** value from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="95f7e-203">In the **Identity Provider Issuer** box, enter the **SAML Entity ID** value from the Azure AD application configuration window.</span></span>
  3. <span data-ttu-id="95f7e-204">Open the downloaded certificate file in Notepad, copy the content, and then paste it in the **Public Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="95f7e-204">Open the downloaded certificate file in Notepad, copy the content, and then paste it in the **Public Certificate** box.</span></span>
  4. <span data-ttu-id="95f7e-205">Configure the preceding three settings as appropriate for your Slack team.</span><span class="sxs-lookup"><span data-stu-id="95f7e-205">Configure the preceding three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="95f7e-206">For more information about the settings, see the [Guide to single sign-on with Slack](https://get.slack.help/hc/en-us/articles/220403548-Guide-to-single-sign-on-with-Slack).</span><span class="sxs-lookup"><span data-stu-id="95f7e-206">For more information about the settings, see the [Guide to single sign-on with Slack](https://get.slack.help/hc/en-us/articles/220403548-Guide-to-single-sign-on-with-Slack).</span></span>
  5. <span data-ttu-id="95f7e-207">Click **Save Configuration**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-207">Click **Save Configuration**.</span></span>
  6. <span data-ttu-id="95f7e-208">Deselect **Allow users to change their email address**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-208">Deselect **Allow users to change their email address**.</span></span>
  7. <span data-ttu-id="95f7e-209">Select **Allow users to choose their own username**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-209">Select **Allow users to choose their own username**.</span></span>
  8. <span data-ttu-id="95f7e-210">As **Authentication for your team must be used by**, select **It’s optional**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-210">As **Authentication for your team must be used by**, select **It’s optional**.</span></span>
  
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="95f7e-211">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="95f7e-211">Create an Azure AD test user</span></span>
<span data-ttu-id="95f7e-212">In this section, you create a test user in the Azure portal called Britta Simon by doing the following:</span><span class="sxs-lookup"><span data-stu-id="95f7e-212">In this section, you create a test user in the Azure portal called Britta Simon by doing the following:</span></span>

1. <span data-ttu-id="95f7e-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="95f7e-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The "Azure Active Directory" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="95f7e-215">Go to **Users and groups**, and then click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="95f7e-215">Go to **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![The Azure AD "All users" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="95f7e-217">At the top of the **All users** dialog box, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-217">At the top of the **All users** dialog box, click **Add**.</span></span>

    ![The "Add" button in the Add users dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="95f7e-219">In the **User** dialog box, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="95f7e-219">In the **User** dialog box, enter the following information:</span></span>

    ![The "User" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/create_aaduser_04.png)
  1. <span data-ttu-id="95f7e-221">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-221">In the **Name** box, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="95f7e-222">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95f7e-222">In the **User name** box, type the email address of user Britta Simon.</span></span>
  3. <span data-ttu-id="95f7e-223">Select the **Show Password** check box, and then write down the value that's shown in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="95f7e-223">Select the **Show Password** check box, and then write down the value that's shown in the **Password** box.</span></span>
  4. <span data-ttu-id="95f7e-224">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-224">Click **Create**.</span></span>

### <a name="create-a-slack-test-user"></a><span data-ttu-id="95f7e-225">Create a Slack test user</span><span class="sxs-lookup"><span data-stu-id="95f7e-225">Create a Slack test user</span></span>

<span data-ttu-id="95f7e-226">In this section, a user called Britta Simon is created in Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-226">In this section, a user called Britta Simon is created in Slack.</span></span> <span data-ttu-id="95f7e-227">Slack supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="95f7e-227">Slack supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="95f7e-228">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="95f7e-228">There is no action item for you in this section.</span></span> <span data-ttu-id="95f7e-229">If a user doesn't already exist in Slack, a new one is created when you attempt to access Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-229">If a user doesn't already exist in Slack, a new one is created when you attempt to access Slack.</span></span>

>[!NOTE]
><span data-ttu-id="95f7e-230">If you need to create a user manually, contact the [Slack support team](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="95f7e-230">If you need to create a user manually, contact the [Slack support team](https://slack.com/help/contact).</span></span>
>
>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="95f7e-231">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="95f7e-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="95f7e-232">In this section, you enable user Britta Simon to use Azure SSO by granting it access to Slack.</span><span class="sxs-lookup"><span data-stu-id="95f7e-232">In this section, you enable user Britta Simon to use Azure SSO by granting it access to Slack.</span></span>

![Assign a user of Azure SSO][200]

<span data-ttu-id="95f7e-234">To assign user Britta Simon to Slack, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="95f7e-234">To assign user Britta Simon to Slack, perform the following steps:</span></span>

1. <span data-ttu-id="95f7e-235">In the Azure portal, open the applications view, go to the directory view, go to **Enterprise applications**, and then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-235">In the Azure portal, open the applications view, go to the directory view, go to **Enterprise applications**, and then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="95f7e-237">In the **Applications** list, select **Slack**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-237">In the **Applications** list, select **Slack**.</span></span>

    ![The Azure portal applications list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_slack_50.png)

3. <span data-ttu-id="95f7e-239">In the left pane, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-239">In the left pane, click **Users and groups**.</span></span>

    ![Left-pane "Users and groups" button][202]

4. <span data-ttu-id="95f7e-241">Click the **Add** button and then, on the **Add Assignment** blade, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-241">Click the **Add** button and then, on the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![The "Add" button and "Add Assignment" blade][203]

5. <span data-ttu-id="95f7e-243">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="95f7e-243">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="95f7e-244">Click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="95f7e-244">Click the **Select** button.</span></span>

7. <span data-ttu-id="95f7e-245">On the **Add Assignment** blade, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="95f7e-245">On the **Add Assignment** blade, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="95f7e-246">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="95f7e-246">Test single sign-on</span></span>

<span data-ttu-id="95f7e-247">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="95f7e-247">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="95f7e-248">To test the configuration, go to the Access Panel, and then click the **Slack** tile.</span><span class="sxs-lookup"><span data-stu-id="95f7e-248">To test the configuration, go to the Access Panel, and then click the **Slack** tile.</span></span> <span data-ttu-id="95f7e-249">The user should be automatically signed in to the Slack application.</span><span class="sxs-lookup"><span data-stu-id="95f7e-249">The user should be automatically signed in to the Slack application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="95f7e-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="95f7e-250">Additional resources</span></span>

* [<span data-ttu-id="95f7e-251">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95f7e-251">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95f7e-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95f7e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-tutorial/tutorial_general_203.png































