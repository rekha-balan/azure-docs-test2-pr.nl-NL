---
title: 'Tutorial: Azure Active Directory integration with AirWatch | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f3bbcbb70759e7a995797cf89ad75a2a39314927
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870968"
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="a4234-103">Tutorial: Azure Active Directory integration with AirWatch</span><span class="sxs-lookup"><span data-stu-id="a4234-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="a4234-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4234-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4234-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a4234-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a4234-106">You can control in Azure AD who has access to AirWatch</span><span class="sxs-lookup"><span data-stu-id="a4234-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="a4234-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a4234-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4234-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a4234-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a4234-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a4234-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4234-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4234-110">Prerequisites</span></span>

<span data-ttu-id="a4234-111">To configure Azure AD integration with AirWatch, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a4234-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="a4234-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a4234-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4234-113">An AirWatch single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a4234-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4234-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a4234-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4234-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a4234-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4234-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a4234-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4234-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4234-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4234-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a4234-118">Scenario description</span></span>
<span data-ttu-id="a4234-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a4234-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4234-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a4234-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4234-121">Adding AirWatch from the gallery</span><span class="sxs-lookup"><span data-stu-id="a4234-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="a4234-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a4234-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="a4234-123">Adding AirWatch from the gallery</span><span class="sxs-lookup"><span data-stu-id="a4234-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="a4234-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a4234-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a4234-125">**To add AirWatch from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a4234-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a4234-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a4234-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4234-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a4234-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a4234-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a4234-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a4234-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a4234-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a4234-133">In the search box, type **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="a4234-133">In the search box, type **AirWatch**.</span></span>

    ![Creating an Azure AD test user](./media/airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="a4234-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a4234-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4234-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a4234-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4234-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a4234-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a4234-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4234-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="a4234-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a4234-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="a4234-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span><span class="sxs-lookup"><span data-stu-id="a4234-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="a4234-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a4234-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4234-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a4234-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4234-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4234-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4234-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a4234-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4234-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a4234-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4234-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a4234-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4234-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a4234-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4234-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span><span class="sxs-lookup"><span data-stu-id="a4234-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="a4234-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a4234-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="a4234-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a4234-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="a4234-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a4234-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="a4234-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="a4234-157">a.</span><span class="sxs-lookup"><span data-stu-id="a4234-157">a.</span></span> <span data-ttu-id="a4234-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="a4234-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="a4234-159">b.</span><span class="sxs-lookup"><span data-stu-id="a4234-159">b.</span></span> <span data-ttu-id="a4234-160">In the **Identifier** textbox, type the value as `AirWatch`</span><span class="sxs-lookup"><span data-stu-id="a4234-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a4234-161">This value is not the real.</span><span class="sxs-lookup"><span data-stu-id="a4234-161">This value is not the real.</span></span> <span data-ttu-id="a4234-162">Update this value with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="a4234-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="a4234-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="a4234-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="a4234-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a4234-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="a4234-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a4234-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a4234-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a4234-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="a4234-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a4234-169">Click **Save** button.</span></span>

    <span data-ttu-id="a4234-170">![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="a4234-170">![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="a4234-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a4234-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="a4234-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span><span class="sxs-lookup"><span data-stu-id="a4234-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="a4234-173">![Administrators](./media/airwatch-tutorial/ic791920.png "Administrators")</span><span class="sxs-lookup"><span data-stu-id="a4234-173">![Administrators](./media/airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="a4234-174">Expand the **Settings** menu, and then click **Directory Services**.</span><span class="sxs-lookup"><span data-stu-id="a4234-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="a4234-175">![Settings](./media/airwatch-tutorial/ic791921.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="a4234-175">![Settings](./media/airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="a4234-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a4234-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="a4234-177">![User](./media/airwatch-tutorial/ic791922.png "User")</span><span class="sxs-lookup"><span data-stu-id="a4234-177">![User](./media/airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="a4234-178">Click the **Server** tab.</span><span class="sxs-lookup"><span data-stu-id="a4234-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="a4234-179">![Server](./media/airwatch-tutorial/ic791923.png "Server")</span><span class="sxs-lookup"><span data-stu-id="a4234-179">![Server](./media/airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="a4234-180">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="a4234-181">![Upload](./media/airwatch-tutorial/ic791924.png "Upload")</span><span class="sxs-lookup"><span data-stu-id="a4234-181">![Upload](./media/airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="a4234-182">a.</span><span class="sxs-lookup"><span data-stu-id="a4234-182">a.</span></span> <span data-ttu-id="a4234-183">As **Directory Type**, select **None**.</span><span class="sxs-lookup"><span data-stu-id="a4234-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="a4234-184">b.</span><span class="sxs-lookup"><span data-stu-id="a4234-184">b.</span></span> <span data-ttu-id="a4234-185">Select **Use SAML For Authentication**.</span><span class="sxs-lookup"><span data-stu-id="a4234-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="a4234-186">c.</span><span class="sxs-lookup"><span data-stu-id="a4234-186">c.</span></span> <span data-ttu-id="a4234-187">To upload the downloaded certificate, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="a4234-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="a4234-188">In the **Request** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="a4234-189">![Request](./media/airwatch-tutorial/ic791925.png "Request")</span><span class="sxs-lookup"><span data-stu-id="a4234-189">![Request](./media/airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="a4234-190">a.</span><span class="sxs-lookup"><span data-stu-id="a4234-190">a.</span></span> <span data-ttu-id="a4234-191">As **Request Binding Type**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="a4234-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="a4234-192">b.</span><span class="sxs-lookup"><span data-stu-id="a4234-192">b.</span></span> <span data-ttu-id="a4234-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="a4234-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="a4234-194">c.</span><span class="sxs-lookup"><span data-stu-id="a4234-194">c.</span></span> <span data-ttu-id="a4234-195">As **NameID Format**, select **Email Address**.</span><span class="sxs-lookup"><span data-stu-id="a4234-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="a4234-196">d.</span><span class="sxs-lookup"><span data-stu-id="a4234-196">d.</span></span> <span data-ttu-id="a4234-197">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a4234-197">Click **Save**.</span></span>

14. <span data-ttu-id="a4234-198">Click the **User** tab again.</span><span class="sxs-lookup"><span data-stu-id="a4234-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="a4234-199">![User](./media/airwatch-tutorial/ic791926.png "User")</span><span class="sxs-lookup"><span data-stu-id="a4234-199">![User](./media/airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="a4234-200">In the **Attribute** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="a4234-201">![Attribute](./media/airwatch-tutorial/ic791927.png "Attribute")</span><span class="sxs-lookup"><span data-stu-id="a4234-201">![Attribute](./media/airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="a4234-202">a.</span><span class="sxs-lookup"><span data-stu-id="a4234-202">a.</span></span> <span data-ttu-id="a4234-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="a4234-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="a4234-204">b.</span><span class="sxs-lookup"><span data-stu-id="a4234-204">b.</span></span> <span data-ttu-id="a4234-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="a4234-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="a4234-206">c.</span><span class="sxs-lookup"><span data-stu-id="a4234-206">c.</span></span> <span data-ttu-id="a4234-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="a4234-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="a4234-208">d.</span><span class="sxs-lookup"><span data-stu-id="a4234-208">d.</span></span> <span data-ttu-id="a4234-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="a4234-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="a4234-210">e.</span><span class="sxs-lookup"><span data-stu-id="a4234-210">e.</span></span> <span data-ttu-id="a4234-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="a4234-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="a4234-212">f.</span><span class="sxs-lookup"><span data-stu-id="a4234-212">f.</span></span> <span data-ttu-id="a4234-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="a4234-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="a4234-214">g.</span><span class="sxs-lookup"><span data-stu-id="a4234-214">g.</span></span> <span data-ttu-id="a4234-215">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a4234-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4234-216">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a4234-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4234-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4234-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a4234-219">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a4234-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4234-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a4234-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4234-222">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a4234-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4234-224">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a4234-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4234-226">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4234-228">a.</span><span class="sxs-lookup"><span data-stu-id="a4234-228">a.</span></span> <span data-ttu-id="a4234-229">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4234-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4234-230">b.</span><span class="sxs-lookup"><span data-stu-id="a4234-230">b.</span></span> <span data-ttu-id="a4234-231">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4234-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a4234-232">c.</span><span class="sxs-lookup"><span data-stu-id="a4234-232">c.</span></span> <span data-ttu-id="a4234-233">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a4234-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a4234-234">d.</span><span class="sxs-lookup"><span data-stu-id="a4234-234">d.</span></span> <span data-ttu-id="a4234-235">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a4234-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="a4234-236">Creating a AirWatch test user</span><span class="sxs-lookup"><span data-stu-id="a4234-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="a4234-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span><span class="sxs-lookup"><span data-stu-id="a4234-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="a4234-238">When AirWatch, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a4234-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="a4234-239">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a4234-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a4234-240">Log in to your **AirWatch** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="a4234-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="a4234-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="a4234-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="a4234-242">![Users](./media/airwatch-tutorial/ic791929.png "Users")</span><span class="sxs-lookup"><span data-stu-id="a4234-242">![Users](./media/airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="a4234-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="a4234-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="a4234-244">![Add User](./media/airwatch-tutorial/ic791930.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="a4234-244">![Add User](./media/airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="a4234-245">On the **Add / Edit User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a4234-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="a4234-246">![Add User](./media/airwatch-tutorial/ic791931.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="a4234-246">![Add User](./media/airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="a4234-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="a4234-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="a4234-248">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a4234-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a4234-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a4234-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a4234-250">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a4234-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a4234-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span><span class="sxs-lookup"><span data-stu-id="a4234-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Assign User][200] 

<span data-ttu-id="a4234-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a4234-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="a4234-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a4234-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a4234-256">In the applications list, select **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="a4234-256">In the applications list, select **AirWatch**.</span></span>

    ![Configure Single Sign-On](./media/airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="a4234-258">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a4234-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="a4234-260">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a4234-260">Click **Add** button.</span></span> <span data-ttu-id="a4234-261">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a4234-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="a4234-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a4234-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a4234-264">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a4234-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4234-265">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a4234-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4234-266">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a4234-266">Testing single sign-on</span></span>

<span data-ttu-id="a4234-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a4234-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a4234-268">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a4234-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a4234-269">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4234-269">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a4234-270">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a4234-270">Additional resources</span></span>

* [<span data-ttu-id="a4234-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4234-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a4234-272">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4234-272">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/airwatch-tutorial/tutorial_general_01.png
[2]: ./media/airwatch-tutorial/tutorial_general_02.png
[3]: ./media/airwatch-tutorial/tutorial_general_03.png
[4]: ./media/airwatch-tutorial/tutorial_general_04.png

[100]: ./media/airwatch-tutorial/tutorial_general_100.png

[200]: ./media/airwatch-tutorial/tutorial_general_200.png
[201]: ./media/airwatch-tutorial/tutorial_general_201.png
[202]: ./media/airwatch-tutorial/tutorial_general_202.png
[203]: ./media/airwatch-tutorial/tutorial_general_203.png

