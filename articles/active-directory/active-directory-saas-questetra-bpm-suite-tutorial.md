---
title: 'Tutorial: Azure Active Directory integration with Questetra BPM Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Questetra BPM Suite.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: fa59290d50e091510498b25a9782c9a9579b8032
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550669"
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="9ac2a-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="9ac2a-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="9ac2a-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ac2a-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="9ac2a-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="9ac2a-106">You can control in Azure AD who has access to Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="9ac2a-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="9ac2a-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9ac2a-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="9ac2a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="9ac2a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="9ac2a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ac2a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ac2a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ac2a-110">Prerequisites</span></span>
<span data-ttu-id="9ac2a-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="9ac2a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9ac2a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="9ac2a-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9ac2a-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ac2a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="9ac2a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9ac2a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9ac2a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ac2a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="9ac2a-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="9ac2a-118">Scenario Description</span></span>
<span data-ttu-id="9ac2a-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="9ac2a-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="9ac2a-121">Adding Questetra BPM Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="9ac2a-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="9ac2a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ac2a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="9ac2a-123">Adding Questetra BPM Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="9ac2a-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="9ac2a-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ac2a-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ac2a-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ac2a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="9ac2a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9ac2a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="9ac2a-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="9ac2a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="9ac2a-135">In the search box, type **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="9ac2a-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ac2a-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ac2a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ac2a-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9ac2a-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ac2a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="9ac2a-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="9ac2a-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="9ac2a-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ac2a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ac2a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ac2a-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9ac2a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ac2a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ac2a-149">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9ac2a-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="9ac2a-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="9ac2a-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ac2a-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="9ac2a-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][8]

2. <span data-ttu-id="9ac2a-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]

3. <span data-ttu-id="9ac2a-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="9ac2a-157">In the menu on the top, click **System Settings**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

5. <span data-ttu-id="9ac2a-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

6. <span data-ttu-id="9ac2a-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure App Settings][13]
   
    <span data-ttu-id="9ac2a-163">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-163">a.</span></span> <span data-ttu-id="9ac2a-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-165">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-165">b.</span></span> <span data-ttu-id="9ac2a-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-167">c.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-167">c.</span></span> <span data-ttu-id="9ac2a-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-169">d.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-169">d.</span></span> <span data-ttu-id="9ac2a-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-170">Click **Next**.</span></span>

7. <span data-ttu-id="9ac2a-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configure Single Sign-On][14]

8. <span data-ttu-id="9ac2a-173">On you **Questetra BPM Suite** company site, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][15]
   
    <span data-ttu-id="9ac2a-175">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-175">a.</span></span> <span data-ttu-id="9ac2a-176">Select **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="9ac2a-177">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-177">b.</span></span> <span data-ttu-id="9ac2a-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-179">c.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-179">c.</span></span> <span data-ttu-id="9ac2a-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-181">d.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-181">d.</span></span> <span data-ttu-id="9ac2a-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="9ac2a-183">e.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-183">e.</span></span> <span data-ttu-id="9ac2a-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="9ac2a-185">f.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-185">f.</span></span> <span data-ttu-id="9ac2a-186">Create a base-64 encoded file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="9ac2a-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="9ac2a-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="9ac2a-188">g.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-188">g.</span></span> <span data-ttu-id="9ac2a-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="9ac2a-190">h.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-190">h.</span></span> <span data-ttu-id="9ac2a-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-191">Click **Save**.</span></span>

1. <span data-ttu-id="9ac2a-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![What is Azure AD Connect][17]

2. <span data-ttu-id="9ac2a-194">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![What is Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ac2a-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9ac2a-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ac2a-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="9ac2a-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ac2a-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ac2a-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Create Azure AD test user][100] 

2. <span data-ttu-id="9ac2a-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9ac2a-202">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Create Azure AD test user][101] 

4. <span data-ttu-id="9ac2a-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Create Azure AD test user][102] 

5. <span data-ttu-id="9ac2a-206">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Create Azure AD test user][103]
   
    <span data-ttu-id="9ac2a-208">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-208">a.</span></span> <span data-ttu-id="9ac2a-209">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="9ac2a-210">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-210">b.</span></span> <span data-ttu-id="9ac2a-211">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="9ac2a-212">c.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-212">c.</span></span> <span data-ttu-id="9ac2a-213">Click Next.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-213">Click Next.</span></span>

6. <span data-ttu-id="9ac2a-214">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Create Azure AD test user][104] 
   
    <span data-ttu-id="9ac2a-216">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-216">a.</span></span> <span data-ttu-id="9ac2a-217">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="9ac2a-218">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-218">b.</span></span> <span data-ttu-id="9ac2a-219">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="9ac2a-220">c.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-220">c.</span></span> <span data-ttu-id="9ac2a-221">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="9ac2a-222">d.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-222">d.</span></span> <span data-ttu-id="9ac2a-223">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="9ac2a-224">e.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-224">e.</span></span> <span data-ttu-id="9ac2a-225">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-225">Click **Next**.</span></span>

7. <span data-ttu-id="9ac2a-226">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Create Azure AD test user][105]  

8. <span data-ttu-id="9ac2a-228">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Create Azure AD test user][106]   
   
    <span data-ttu-id="9ac2a-230">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-230">a.</span></span> <span data-ttu-id="9ac2a-231">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="9ac2a-232">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-232">b.</span></span> <span data-ttu-id="9ac2a-233">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="9ac2a-234">Creating a Questetra BPM Suite test user</span><span class="sxs-lookup"><span data-stu-id="9ac2a-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="9ac2a-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="9ac2a-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ac2a-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="9ac2a-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="9ac2a-238">Go to **System Settings > User List > New User**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="9ac2a-239">On the New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ac2a-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Create test user][300] 
   
    <span data-ttu-id="9ac2a-241">a.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-241">a.</span></span> <span data-ttu-id="9ac2a-242">In the **Name** textbox, type Britta's user name in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="9ac2a-243">b.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-243">b.</span></span> <span data-ttu-id="9ac2a-244">In the **Email** textbox, type Britta's user name in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="9ac2a-245">c.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-245">c.</span></span> <span data-ttu-id="9ac2a-246">In the **Password** textbox, type a password.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="9ac2a-247">Click **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9ac2a-248">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9ac2a-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="9ac2a-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![What is Azure AD Connect][200]

<span data-ttu-id="9ac2a-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ac2a-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="9ac2a-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![What is Azure AD Connect][201]
2. <span data-ttu-id="9ac2a-254">In the applications list, select **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![What is Azure AD Connect][205]
3. <span data-ttu-id="9ac2a-256">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-256">In the menu on the top, click **Users**.</span></span>
   
    ![What is Azure AD Connect][202]
4. <span data-ttu-id="9ac2a-258">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![What is Azure AD Connect][203]
5. <span data-ttu-id="9ac2a-260">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![What is Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="9ac2a-262">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9ac2a-262">Testing Single Sign-On</span></span>
<span data-ttu-id="9ac2a-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="9ac2a-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span><span class="sxs-lookup"><span data-stu-id="9ac2a-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ac2a-265">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="9ac2a-265">Additional Resources</span></span>
* [<span data-ttu-id="9ac2a-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ac2a-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ac2a-267">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ac2a-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 






























