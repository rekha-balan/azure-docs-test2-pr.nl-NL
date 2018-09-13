---
title: 'Tutorial: Azure Active Directory integration with Proofpoint on Demand | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Proofpoint on Demand.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: de2182dea5e5d00ce0acd3b73c9853bdfc891aa2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563442"
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="21ed0-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="21ed0-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>
<span data-ttu-id="21ed0-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21ed0-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21ed0-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="21ed0-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="21ed0-106">You can control in Azure AD who has access to Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="21ed0-106">You can control in Azure AD who has access to Proofpoint on Demand.</span></span>
* <span data-ttu-id="21ed0-107">You can enable your users to automatically get signed on to Proofpoint on Demand (single sign-on, or SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="21ed0-107">You can enable your users to automatically get signed on to Proofpoint on Demand (single sign-on, or SSO) with their Azure AD accounts.</span></span>
* <span data-ttu-id="21ed0-108">You can manage your accounts in one central location, the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="21ed0-108">You can manage your accounts in one central location, the Azure classic portal.</span></span>

<span data-ttu-id="21ed0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21ed0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21ed0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21ed0-110">Prerequisites</span></span>
<span data-ttu-id="21ed0-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="21ed0-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

* <span data-ttu-id="21ed0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="21ed0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="21ed0-113">A Proofpoint on Demand single sign-on (SSO) subscription</span><span class="sxs-lookup"><span data-stu-id="21ed0-113">A Proofpoint on Demand single sign-on (SSO) subscription</span></span>

<span data-ttu-id="21ed0-114">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="21ed0-114">To test the steps in this tutorial, follow these recommendations:</span></span>

* <span data-ttu-id="21ed0-115">Don't use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="21ed0-115">Don't use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="21ed0-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21ed0-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21ed0-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="21ed0-117">Scenario description</span></span>
<span data-ttu-id="21ed0-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="21ed0-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="21ed0-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="21ed0-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="21ed0-120">Add Proofpoint on Demand from the gallery.</span><span class="sxs-lookup"><span data-stu-id="21ed0-120">Add Proofpoint on Demand from the gallery.</span></span>
* <span data-ttu-id="21ed0-121">Configure and test Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="21ed0-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="21ed0-122">Add Proofpoint on Demand from the gallery</span><span class="sxs-lookup"><span data-stu-id="21ed0-122">Add Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="21ed0-123">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="21ed0-123">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="21ed0-124">In the Azure classic portal, in the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-124">In the Azure classic portal, in the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory icon][1]
2. <span data-ttu-id="21ed0-126">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="21ed0-126">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="21ed0-127">To open the applications view, in the directory view, click **APPLICATIONS** on the menu at the top.</span><span class="sxs-lookup"><span data-stu-id="21ed0-127">To open the applications view, in the directory view, click **APPLICATIONS** on the menu at the top.</span></span>
   
    ![APPLICATIONS menu item][2]
4. <span data-ttu-id="21ed0-129">Click **ADD** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="21ed0-129">Click **ADD** at the bottom of the page.</span></span>
   
    ![ADD button][3]
5. <span data-ttu-id="21ed0-131">In the **What do you want to do** dialog box, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-131">In the **What do you want to do** dialog box, click **Add an application from the gallery**.</span></span>
   
    ![Choice of adding an application from the gallery][4]
6. <span data-ttu-id="21ed0-133">In the search box, type **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-133">In the search box, type **Proofpoint on Demand**.</span></span>
   
    ![Box where you type "Proofpoint on Demand"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_01.png)
7. <span data-ttu-id="21ed0-135">In the results pane, select **Proofpoint on Demand**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="21ed0-135">In the results pane, select **Proofpoint on Demand**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="21ed0-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="21ed0-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="21ed0-137">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user named Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21ed0-137">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user named Britta Simon.</span></span>

<span data-ttu-id="21ed0-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21ed0-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="21ed0-139">In other words, you need to establish a link relationship between an Azure AD user and the related user in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="21ed0-139">In other words, you need to establish a link relationship between an Azure AD user and the related user in Proofpoint on Demand.</span></span>

<span data-ttu-id="21ed0-140">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="21ed0-140">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="21ed0-141">To configure and test Azure AD single sign-on with Proofpoint on Demand, complete the following procedures:</span><span class="sxs-lookup"><span data-stu-id="21ed0-141">To configure and test Azure AD single sign-on with Proofpoint on Demand, complete the following procedures:</span></span>

1. <span data-ttu-id="21ed0-142">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on), to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="21ed0-142">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on), to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21ed0-143">[Create an Azure AD test user](#creating-an-azure-ad-test-user), to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21ed0-143">[Create an Azure AD test user](#creating-an-azure-ad-test-user), to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21ed0-144">[Create a Proofpoint on Demand test user](#creating-a-proofpoint-ondemand-test-user), to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="21ed0-144">[Create a Proofpoint on Demand test user](#creating-a-proofpoint-ondemand-test-user), to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="21ed0-145">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user), to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="21ed0-145">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user), to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21ed0-146">[Test single sign-on](#testing-single-sign-on), to verify that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="21ed0-146">[Test single sign-on](#testing-single-sign-on), to verify that the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="21ed0-147">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="21ed0-147">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="21ed0-148">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Proofpoint on Demand application.</span><span class="sxs-lookup"><span data-stu-id="21ed0-148">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

1. <span data-ttu-id="21ed0-149">In the classic portal, on the **Proofpoint on Demand** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog box.</span><span class="sxs-lookup"><span data-stu-id="21ed0-149">In the classic portal, on the **Proofpoint on Demand** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog box.</span></span>
   
    !["Configure single sign-on" button][6]
2. <span data-ttu-id="21ed0-151">On the **How would you like users to sign on to Proofpoint on Demand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-151">On the **How would you like users to sign on to Proofpoint on Demand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    !["Microsoft Azure AD Single Sign-On" option button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_03.png)
3. <span data-ttu-id="21ed0-153">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="21ed0-153">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    !["Configure App Settings" page with boxes filled in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_04.png)
   1. <span data-ttu-id="21ed0-155">In the **SIGN ON URL** box, type the URL where users sign on to your Proofpoint on Demand application.</span><span class="sxs-lookup"><span data-stu-id="21ed0-155">In the **SIGN ON URL** box, type the URL where users sign on to your Proofpoint on Demand application.</span></span> <span data-ttu-id="21ed0-156">Use the following pattern: **https://\<hostname\>.pphosted.com/ppssamlsp_hostname**</span><span class="sxs-lookup"><span data-stu-id="21ed0-156">Use the following pattern: **https://\<hostname\>.pphosted.com/ppssamlsp_hostname**</span></span>
   2. <span data-ttu-id="21ed0-157">In the **IDENTIFIER** box, type the URL by using the following pattern: **https://\<hostname/>.pphosted.com/ppssamlsp**</span><span class="sxs-lookup"><span data-stu-id="21ed0-157">In the **IDENTIFIER** box, type the URL by using the following pattern: **https://\<hostname/>.pphosted.com/ppssamlsp**</span></span>
   3. <span data-ttu-id="21ed0-158">In the **REPLY URL** box, type the URL by using the following pattern: **https://\<hostname/>.pphosted.com:portnumber/v1/samlauth/samlconsumer**</span><span class="sxs-lookup"><span data-stu-id="21ed0-158">In the **REPLY URL** box, type the URL by using the following pattern: **https://\<hostname/>.pphosted.com:portnumber/v1/samlauth/samlconsumer**</span></span>  
   4. <span data-ttu-id="21ed0-159">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-159">Click **Next**.</span></span>
4. <span data-ttu-id="21ed0-160">On the **Configure single sign-on at Proofpoint on Demand** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="21ed0-160">On the **Configure single sign-on at Proofpoint on Demand** page, perform the following steps:</span></span>
   
    !["Configure single sign-on at Proofpoint on Demand" page with "Download certificate" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_05.png)
   1. <span data-ttu-id="21ed0-162">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="21ed0-162">Click **Download certificate**, and then save the file on your computer.</span></span>   
   2. <span data-ttu-id="21ed0-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-163">Click **Next**.</span></span>
5. <span data-ttu-id="21ed0-164">To get SSO configured for your application, contact the Proofpoint on Demand support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="21ed0-164">To get SSO configured for your application, contact the Proofpoint on Demand support team and provide them with the following:</span></span>
   * <span data-ttu-id="21ed0-165">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="21ed0-165">The downloaded certificate</span></span>
   * <span data-ttu-id="21ed0-166">The entity ID</span><span class="sxs-lookup"><span data-stu-id="21ed0-166">The entity ID</span></span>
   * <span data-ttu-id="21ed0-167">The SAML SSO URL</span><span class="sxs-lookup"><span data-stu-id="21ed0-167">The SAML SSO URL</span></span>
6. <span data-ttu-id="21ed0-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Check box that confirms that you have configured single sign-on][10]
7. <span data-ttu-id="21ed0-170">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Confirmation page][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="21ed0-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="21ed0-172">Create an Azure AD test user</span></span>
<span data-ttu-id="21ed0-173">In this section, you create a test user named Britta Simon in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="21ed0-173">In this section, you create a test user named Britta Simon in the classic portal.</span></span>

![The test user in the list of users][20]

1. <span data-ttu-id="21ed0-175">In the Azure classic portal, in the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-175">In the Azure classic portal, in the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="21ed0-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="21ed0-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="21ed0-178">To display the list of users, on the menu at the top, click **USERS**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-178">To display the list of users, on the menu at the top, click **USERS**.</span></span>
   
    ![USERS menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="21ed0-180">To open the **Add User** dialog box, on the toolbar at the bottom, click **ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-180">To open the **Add User** dialog box, on the toolbar at the bottom, click **ADD USER**.</span></span>
   
    ![ADD USER button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="21ed0-182">On the **Tell us about this user** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="21ed0-182">On the **Tell us about this user** page, perform the following steps:</span></span>

    !["Tell us about this user" page with boxes filled in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_05.png)   
   1. <span data-ttu-id="21ed0-184">In the **TYPE OF USER** box, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-184">In the **TYPE OF USER** box, select **New user in your organization**.</span></span>
   2. <span data-ttu-id="21ed0-185">In the **USER NAME** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-185">In the **USER NAME** box, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="21ed0-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-186">Click **Next**.</span></span>
6. <span data-ttu-id="21ed0-187">On the **user profile** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="21ed0-187">On the **user profile** page, perform the following steps:</span></span>

  ![The "user profile" page with boxes filled in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_06.png)   
   1. <span data-ttu-id="21ed0-189">In the **FIRST NAME** box, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-189">In the **FIRST NAME** box, type **Britta**.</span></span>  
   2. <span data-ttu-id="21ed0-190">In the **LAST NAME** box, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-190">In the **LAST NAME** box, type **Simon**.</span></span>
   3. <span data-ttu-id="21ed0-191">In the **DISPLAY NAME** box, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-191">In the **DISPLAY NAME** box, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="21ed0-192">In the **ROLE** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-192">In the **ROLE** list, select **User**.</span></span>
   5. <span data-ttu-id="21ed0-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-193">Click **Next**.</span></span>
7. <span data-ttu-id="21ed0-194">On the **Get temporary password** page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-194">On the **Get temporary password** page, click **create**.</span></span>
   
   ![Button for creating a temporary password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="21ed0-196">On the **Get temporary password** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="21ed0-196">On the **Get temporary password** page, perform the following steps:</span></span>
   
   !["Get temporary password" page with password info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_08.png)  
   1. <span data-ttu-id="21ed0-198">Write down the value in the **NEW PASSWORD** box.</span><span class="sxs-lookup"><span data-stu-id="21ed0-198">Write down the value in the **NEW PASSWORD** box.</span></span>
   2. <span data-ttu-id="21ed0-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-199">Click **Complete**.</span></span>   

### <a name="create-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="21ed0-200">Create a Proofpoint on Demand test user</span><span class="sxs-lookup"><span data-stu-id="21ed0-200">Create a Proofpoint on Demand test user</span></span>
<span data-ttu-id="21ed0-201">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="21ed0-201">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="21ed0-202">Please work with Proofpoint on Demand support team to add users in the Proofpoint on Demand platform.</span><span class="sxs-lookup"><span data-stu-id="21ed0-202">Please work with Proofpoint on Demand support team to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="21ed0-203">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="21ed0-203">Assign the Azure AD test user</span></span>
<span data-ttu-id="21ed0-204">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="21ed0-204">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Proofpoint on Demand.</span></span>

![User info, showing access enabled through the direct method][200]

1. <span data-ttu-id="21ed0-206">In the classic portal, in the directory view, click **APPLICATIONS** on the menu at the top to open the applications view.</span><span class="sxs-lookup"><span data-stu-id="21ed0-206">In the classic portal, in the directory view, click **APPLICATIONS** on the menu at the top to open the applications view.</span></span>
   
    ![APPLICATIONS menu item][201]
2. <span data-ttu-id="21ed0-208">In the list of applications, select **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-208">In the list of applications, select **Proofpoint on Demand**.</span></span>
   
    ![List of applications with Proofpoint on Demand selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_50.png)
3. <span data-ttu-id="21ed0-210">On the menu at the top, click **USERS**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-210">On the menu at the top, click **USERS**.</span></span>
   
    ![USERS menu item][203]
4. <span data-ttu-id="21ed0-212">In the list of users, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-212">In the list of users, select **Britta Simon**.</span></span>
5. <span data-ttu-id="21ed0-213">On the toolbar at the bottom, click **ASSIGN**.</span><span class="sxs-lookup"><span data-stu-id="21ed0-213">On the toolbar at the bottom, click **ASSIGN**.</span></span>
   
    ![Assign button][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="21ed0-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="21ed0-215">Test single sign-on</span></span>
<span data-ttu-id="21ed0-216">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="21ed0-216">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="21ed0-217">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span><span class="sxs-lookup"><span data-stu-id="21ed0-217">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21ed0-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="21ed0-218">Additional resources</span></span>
* [<span data-ttu-id="21ed0-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21ed0-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21ed0-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="21ed0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_205.png
























