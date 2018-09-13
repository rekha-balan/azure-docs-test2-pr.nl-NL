---
title: Customize a UI by using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Learn about customizing a user interface (UI) while you use custom policies in Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 9908a7cf96c56e414e0a8d7faea0352b60214ea4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869266"
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="606a3-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span><span class="sxs-lookup"><span data-stu-id="606a3-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="606a3-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span><span class="sxs-lookup"><span data-stu-id="606a3-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="606a3-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span><span class="sxs-lookup"><span data-stu-id="606a3-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="606a3-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="606a3-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="606a3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="606a3-107">Prerequisites</span></span>

<span data-ttu-id="606a3-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="606a3-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="606a3-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span><span class="sxs-lookup"><span data-stu-id="606a3-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="606a3-110">Page UI customization</span><span class="sxs-lookup"><span data-stu-id="606a3-110">Page UI customization</span></span>

<span data-ttu-id="606a3-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span><span class="sxs-lookup"><span data-stu-id="606a3-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="606a3-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="606a3-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="606a3-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="606a3-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="606a3-114">First, you specify a URL in the custom policy with customized HTML content.</span><span class="sxs-lookup"><span data-stu-id="606a3-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="606a3-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span><span class="sxs-lookup"><span data-stu-id="606a3-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="606a3-116">Create your HTML5 content</span><span class="sxs-lookup"><span data-stu-id="606a3-116">Create your HTML5 content</span></span>

<span data-ttu-id="606a3-117">Create HTML content with your product's brand name in the title.</span><span class="sxs-lookup"><span data-stu-id="606a3-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="606a3-118">Copy the following HTML snippet.</span><span class="sxs-lookup"><span data-stu-id="606a3-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="606a3-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span><span class="sxs-lookup"><span data-stu-id="606a3-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="606a3-120">This element indicates where Azure AD B2C content is to be inserted.</span><span class="sxs-lookup"><span data-stu-id="606a3-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="606a3-121">For security reasons, the use of JavaScript is currently blocked for customization.</span><span class="sxs-lookup"><span data-stu-id="606a3-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="606a3-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span><span class="sxs-lookup"><span data-stu-id="606a3-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="606a3-123">Create an Azure Blob storage account</span><span class="sxs-lookup"><span data-stu-id="606a3-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="606a3-124">In this article, we use Azure Blob storage to host our content.</span><span class="sxs-lookup"><span data-stu-id="606a3-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="606a3-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="606a3-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="606a3-126">To host this HTML content in Blob storage, do the following:</span><span class="sxs-lookup"><span data-stu-id="606a3-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="606a3-127">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="606a3-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="606a3-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="606a3-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="606a3-129">Enter a unique **Name** for your storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="606a3-130">**Deployment model** can remain **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="606a3-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="606a3-131">Change **Account Kind** to **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="606a3-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="606a3-132">**Performance** can remain **Standard**.</span><span class="sxs-lookup"><span data-stu-id="606a3-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="606a3-133">**Replication** can remain **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="606a3-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="606a3-134">**Access tier** can remain **Hot**.</span><span class="sxs-lookup"><span data-stu-id="606a3-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="606a3-135">**Storage service encryption** can remain **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="606a3-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="606a3-136">Select a **Subscription** for your storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="606a3-137">Create a **Resource group** or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="606a3-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="606a3-138">Select the **Geographic location** for your storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="606a3-139">Click **Create** to create the storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="606a3-140">After the deployment is completed, the **Storage account** blade opens automatically.</span><span class="sxs-lookup"><span data-stu-id="606a3-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="606a3-141">Create a container</span><span class="sxs-lookup"><span data-stu-id="606a3-141">Create a container</span></span>

<span data-ttu-id="606a3-142">To create a public container in Blob storage, do the following:</span><span class="sxs-lookup"><span data-stu-id="606a3-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="606a3-143">Click the **Overview** tab.</span><span class="sxs-lookup"><span data-stu-id="606a3-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="606a3-144">Click **Container**.</span><span class="sxs-lookup"><span data-stu-id="606a3-144">Click **Container**.</span></span>
3. <span data-ttu-id="606a3-145">For **Name**, type **$root**.</span><span class="sxs-lookup"><span data-stu-id="606a3-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="606a3-146">Set **Access type** to **Blob**.</span><span class="sxs-lookup"><span data-stu-id="606a3-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="606a3-147">Click **$root** to open the new container.</span><span class="sxs-lookup"><span data-stu-id="606a3-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="606a3-148">Click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="606a3-148">Click **Upload**.</span></span>
7. <span data-ttu-id="606a3-149">Click the folder icon next to **Select a file**.</span><span class="sxs-lookup"><span data-stu-id="606a3-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="606a3-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span><span class="sxs-lookup"><span data-stu-id="606a3-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="606a3-151">Click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="606a3-151">Click **Upload**.</span></span>
10. <span data-ttu-id="606a3-152">Select the customize-ui.html blob that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="606a3-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="606a3-153">Next to **URL**, click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="606a3-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="606a3-154">In a browser, paste the copied URL, and go to the site.</span><span class="sxs-lookup"><span data-stu-id="606a3-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="606a3-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span><span class="sxs-lookup"><span data-stu-id="606a3-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="606a3-156">Configure CORS</span><span class="sxs-lookup"><span data-stu-id="606a3-156">Configure CORS</span></span>

<span data-ttu-id="606a3-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span><span class="sxs-lookup"><span data-stu-id="606a3-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="606a3-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span><span class="sxs-lookup"><span data-stu-id="606a3-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="606a3-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="606a3-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="606a3-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="606a3-161">On the **Storage** blade, under **Settings**, open **CORS**.</span><span class="sxs-lookup"><span data-stu-id="606a3-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="606a3-162">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="606a3-162">Click **Add**.</span></span>
3. <span data-ttu-id="606a3-163">For **Allowed origins**, type an asterisk (\*).</span><span class="sxs-lookup"><span data-stu-id="606a3-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="606a3-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span><span class="sxs-lookup"><span data-stu-id="606a3-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="606a3-165">For **Allowed headers**, type an asterisk (\*).</span><span class="sxs-lookup"><span data-stu-id="606a3-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="606a3-166">For **Exposed headers**, type an asterisk (\*).</span><span class="sxs-lookup"><span data-stu-id="606a3-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="606a3-167">For **Maximum age (seconds)**, type **200**.</span><span class="sxs-lookup"><span data-stu-id="606a3-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="606a3-168">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="606a3-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="606a3-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="606a3-169">Test CORS</span></span>

<span data-ttu-id="606a3-170">Validate that you're ready by doing the following:</span><span class="sxs-lookup"><span data-stu-id="606a3-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="606a3-171">Go to the [www.test-cors.org](http://www.test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span><span class="sxs-lookup"><span data-stu-id="606a3-171">Go to the [www.test-cors.org](http://www.test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="606a3-172">Click **Send Request**.</span><span class="sxs-lookup"><span data-stu-id="606a3-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="606a3-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span><span class="sxs-lookup"><span data-stu-id="606a3-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="606a3-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span><span class="sxs-lookup"><span data-stu-id="606a3-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="606a3-175">Modify your sign-up or sign-in custom policy</span><span class="sxs-lookup"><span data-stu-id="606a3-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="606a3-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span><span class="sxs-lookup"><span data-stu-id="606a3-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="606a3-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span><span class="sxs-lookup"><span data-stu-id="606a3-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="606a3-178">Replace *your_storage_account* with the name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="606a3-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
        <DataUri>urn:com:microsoft:aad:b2c:elements:idpselection:1.0.0</DataUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="606a3-179">Upload your updated custom policy</span><span class="sxs-lookup"><span data-stu-id="606a3-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="606a3-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="606a3-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="606a3-181">Click **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="606a3-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="606a3-182">Click **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="606a3-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="606a3-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span><span class="sxs-lookup"><span data-stu-id="606a3-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="606a3-184">Test the custom policy by using **Run now**</span><span class="sxs-lookup"><span data-stu-id="606a3-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="606a3-185">On the **Azure AD B2C** blade, go to **All policies**.</span><span class="sxs-lookup"><span data-stu-id="606a3-185">On the **Azure AD B2C** blade, go to **All policies**.</span></span>
2. <span data-ttu-id="606a3-186">Select the custom policy that you uploaded, and click the **Run now** button.</span><span class="sxs-lookup"><span data-stu-id="606a3-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="606a3-187">You should be able to sign up by using an email address.</span><span class="sxs-lookup"><span data-stu-id="606a3-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="606a3-188">Reference</span><span class="sxs-lookup"><span data-stu-id="606a3-188">Reference</span></span>

<span data-ttu-id="606a3-189">You can find sample templates for UI customization here:</span><span class="sxs-lookup"><span data-stu-id="606a3-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="606a3-190">The sample_templates/wingtip folder contains the following HTML files:</span><span class="sxs-lookup"><span data-stu-id="606a3-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="606a3-191">HTML5 template</span><span class="sxs-lookup"><span data-stu-id="606a3-191">HTML5 template</span></span> | <span data-ttu-id="606a3-192">Description</span><span class="sxs-lookup"><span data-stu-id="606a3-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="606a3-193">*phonefactor.html*</span><span class="sxs-lookup"><span data-stu-id="606a3-193">*phonefactor.html*</span></span> | <span data-ttu-id="606a3-194">Use this file as a template for a multi-factor authentication page.</span><span class="sxs-lookup"><span data-stu-id="606a3-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="606a3-195">*resetpassword.html*</span><span class="sxs-lookup"><span data-stu-id="606a3-195">*resetpassword.html*</span></span> | <span data-ttu-id="606a3-196">Use this file as a template for a forgot password page.</span><span class="sxs-lookup"><span data-stu-id="606a3-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="606a3-197">*selfasserted.html*</span><span class="sxs-lookup"><span data-stu-id="606a3-197">*selfasserted.html*</span></span> | <span data-ttu-id="606a3-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span><span class="sxs-lookup"><span data-stu-id="606a3-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="606a3-199">*unified.html*</span><span class="sxs-lookup"><span data-stu-id="606a3-199">*unified.html*</span></span> | <span data-ttu-id="606a3-200">Use this file as a template for a unified sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="606a3-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="606a3-201">*updateprofile.html*</span><span class="sxs-lookup"><span data-stu-id="606a3-201">*updateprofile.html*</span></span> | <span data-ttu-id="606a3-202">Use this file as a template for a profile update page.</span><span class="sxs-lookup"><span data-stu-id="606a3-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="606a3-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="606a3-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="606a3-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span><span class="sxs-lookup"><span data-stu-id="606a3-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="606a3-205">Content definition ID</span><span class="sxs-lookup"><span data-stu-id="606a3-205">Content definition ID</span></span> | <span data-ttu-id="606a3-206">Description</span><span class="sxs-lookup"><span data-stu-id="606a3-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="606a3-207">*api.error*</span><span class="sxs-lookup"><span data-stu-id="606a3-207">*api.error*</span></span> | <span data-ttu-id="606a3-208">**Error page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-208">**Error page**.</span></span> <span data-ttu-id="606a3-209">This page is displayed when an exception or an error is encountered.</span><span class="sxs-lookup"><span data-stu-id="606a3-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="606a3-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="606a3-210">*api.idpselections*</span></span> | <span data-ttu-id="606a3-211">**Identity provider selection page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-211">**Identity provider selection page**.</span></span> <span data-ttu-id="606a3-212">This page contains a list of identity providers that the user can choose from during sign-in.</span><span class="sxs-lookup"><span data-stu-id="606a3-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="606a3-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="606a3-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="606a3-214">*api.idpselections.signup*</span><span class="sxs-lookup"><span data-stu-id="606a3-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="606a3-215">**Identity provider selection for sign-up**.</span><span class="sxs-lookup"><span data-stu-id="606a3-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="606a3-216">This page contains a list of identity providers that the user can choose from during sign-up.</span><span class="sxs-lookup"><span data-stu-id="606a3-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="606a3-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="606a3-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="606a3-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="606a3-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="606a3-219">**Forgot password page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-219">**Forgot password page**.</span></span> <span data-ttu-id="606a3-220">This page contains a form that the user must complete to initiate a password reset.</span><span class="sxs-lookup"><span data-stu-id="606a3-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="606a3-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="606a3-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="606a3-222">**Local account sign-in page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-222">**Local account sign-in page**.</span></span> <span data-ttu-id="606a3-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span><span class="sxs-lookup"><span data-stu-id="606a3-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="606a3-224">The form can contain a text input box and password entry box.</span><span class="sxs-lookup"><span data-stu-id="606a3-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="606a3-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="606a3-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="606a3-226">**Local account sign-up page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-226">**Local account sign-up page**.</span></span> <span data-ttu-id="606a3-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span><span class="sxs-lookup"><span data-stu-id="606a3-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="606a3-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span><span class="sxs-lookup"><span data-stu-id="606a3-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="606a3-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="606a3-229">*api.phonefactor*</span></span> | <span data-ttu-id="606a3-230">**Multi-factor authentication page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="606a3-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span><span class="sxs-lookup"><span data-stu-id="606a3-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="606a3-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="606a3-232">*api.selfasserted*</span></span> | <span data-ttu-id="606a3-233">**Social account sign-up page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-233">**Social account sign-up page**.</span></span> <span data-ttu-id="606a3-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span><span class="sxs-lookup"><span data-stu-id="606a3-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="606a3-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span><span class="sxs-lookup"><span data-stu-id="606a3-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="606a3-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="606a3-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="606a3-237">**Profile update page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-237">**Profile update page**.</span></span> <span data-ttu-id="606a3-238">This page contains a form that users can use to update their profile.</span><span class="sxs-lookup"><span data-stu-id="606a3-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="606a3-239">This page is similar to the social account sign-up page, except for the password entry fields.</span><span class="sxs-lookup"><span data-stu-id="606a3-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="606a3-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="606a3-240">*api.signuporsignin*</span></span> | <span data-ttu-id="606a3-241">**Unified sign-up or sign-in page**.</span><span class="sxs-lookup"><span data-stu-id="606a3-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="606a3-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="606a3-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="606a3-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="606a3-243">Next steps</span></span>

<span data-ttu-id="606a3-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="606a3-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
