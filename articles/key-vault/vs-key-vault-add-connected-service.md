---
title: Add Key Vault support to your ASP.NET project using Visual Studio | Microsoft Docs
description: Use this tutorial to help you learn how to add Key Vault support to an ASP.NET or ASP.NET Core web application.
services: key-vault
author: ghogen
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 04/15/2018
ms.author: ghogen
ms.openlocfilehash: d2ab34b3737ec00e4adc464f6d2255203fb6ae08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866445"
---
# <a name="add-key-vault-to-your-web-application-by-using-visual-studio-connected-services"></a><span data-ttu-id="2595c-103">Add Key Vault to your web application by using Visual Studio Connected Services</span><span class="sxs-lookup"><span data-stu-id="2595c-103">Add Key Vault to your web application by using Visual Studio Connected Services</span></span>

<span data-ttu-id="2595c-104">In this tutorial, you will learn how to easily add everything you need to start using Azure Key Vault to manage your secrets for web projects in Visual Studio, whether you are using ASP.NET Core or any type of ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="2595c-104">In this tutorial, you will learn how to easily add everything you need to start using Azure Key Vault to manage your secrets for web projects in Visual Studio, whether you are using ASP.NET Core or any type of ASP.NET project.</span></span> <span data-ttu-id="2595c-105">By using the Connected Services feature in Visual Studio 2017, you can have Visual Studio automatically add all the NuGet packages and configuration settings you need to connect to Key Vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="2595c-105">By using the Connected Services feature in Visual Studio 2017, you can have Visual Studio automatically add all the NuGet packages and configuration settings you need to connect to Key Vault in Azure.</span></span> 

<span data-ttu-id="2595c-106">For details on the changes that Connected Services makes in your project to enable Key Vault, see [Key Vault Connected Service - What happened to my ASP.NET 4.7.1 project](vs-key-vault-aspnet-what-happened.md) or [Key Vault Connected Service - What happened to my ASP.NET Core project](vs-key-vault-aspnet-core-what-happened.md).</span><span class="sxs-lookup"><span data-stu-id="2595c-106">For details on the changes that Connected Services makes in your project to enable Key Vault, see [Key Vault Connected Service - What happened to my ASP.NET 4.7.1 project](vs-key-vault-aspnet-what-happened.md) or [Key Vault Connected Service - What happened to my ASP.NET Core project](vs-key-vault-aspnet-core-what-happened.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2595c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2595c-107">Prerequisites</span></span>

- <span data-ttu-id="2595c-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="2595c-108">**An Azure subscription**.</span></span> <span data-ttu-id="2595c-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2595c-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="2595c-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span><span class="sxs-lookup"><span data-stu-id="2595c-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span></span> <span data-ttu-id="2595c-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="2595c-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>
- <span data-ttu-id="2595c-112">For ASP.NET (not Core), you need the .NET Framework 4.7.1 Development Tools, which are not installed by default.</span><span class="sxs-lookup"><span data-stu-id="2595c-112">For ASP.NET (not Core), you need the .NET Framework 4.7.1 Development Tools, which are not installed by default.</span></span> <span data-ttu-id="2595c-113">To install them, launch the Visual Studio Installer, choose **Modify**, and then choose **Individual Components**, then on the right-hand side, expand **ASP.NET and web development**, and choose **.NET Framework 4.7.1 Development Tools**.</span><span class="sxs-lookup"><span data-stu-id="2595c-113">To install them, launch the Visual Studio Installer, choose **Modify**, and then choose **Individual Components**, then on the right-hand side, expand **ASP.NET and web development**, and choose **.NET Framework 4.7.1 Development Tools**.</span></span>
- <span data-ttu-id="2595c-114">An ASP.NET 4.7.1 or ASP.NET Core 2.0 web project open.</span><span class="sxs-lookup"><span data-stu-id="2595c-114">An ASP.NET 4.7.1 or ASP.NET Core 2.0 web project open.</span></span>

## <a name="add-key-vault-support-to-your-project"></a><span data-ttu-id="2595c-115">Add Key Vault support to your project</span><span class="sxs-lookup"><span data-stu-id="2595c-115">Add Key Vault support to your project</span></span>

1. <span data-ttu-id="2595c-116">In **Solution Explorer**, choose **Add** > **Connected Service**.</span><span class="sxs-lookup"><span data-stu-id="2595c-116">In **Solution Explorer**, choose **Add** > **Connected Service**.</span></span>
   <span data-ttu-id="2595c-117">The Connected Service page appears with services you can add to your project.</span><span class="sxs-lookup"><span data-stu-id="2595c-117">The Connected Service page appears with services you can add to your project.</span></span>
1. <span data-ttu-id="2595c-118">In the menu of available services, choose **Secure Secrets With Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="2595c-118">In the menu of available services, choose **Secure Secrets With Azure Key Vault**.</span></span>

   ![Choose "Secure Secrets With Azure Key Vault"](media/vs-key-vault-add-connected-service/KeyVaultConnectedService1.PNG)

   <span data-ttu-id="2595c-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2595c-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span></span>
1. <span data-ttu-id="2595c-121">Select the subscription you want to use, and then choose a new or existing Key Vault, or choose the Edit link to modify the automatically generated name.</span><span class="sxs-lookup"><span data-stu-id="2595c-121">Select the subscription you want to use, and then choose a new or existing Key Vault, or choose the Edit link to modify the automatically generated name.</span></span>

   ![Select your subscription](media/vs-key-vault-add-connected-service/KeyVaultConnectedService3.PNG)

1. <span data-ttu-id="2595c-123">Type the name you want to use for the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2595c-123">Type the name you want to use for the Key Vault.</span></span>

   ![Rename the Key Vault and choose a resource group](media/vs-key-vault-add-connected-service/KeyVaultConnectedService-Edit.PNG)

1. <span data-ttu-id="2595c-125">Select an existing Resource Group, or choose to create a new one with an automatically generated unqiue name.</span><span class="sxs-lookup"><span data-stu-id="2595c-125">Select an existing Resource Group, or choose to create a new one with an automatically generated unqiue name.</span></span>  <span data-ttu-id="2595c-126">If you want to create a new group with a different name, you can use the [Azure Portal](https://portal.azure.com), and then close the page and restart to reload the list of resource groups.</span><span class="sxs-lookup"><span data-stu-id="2595c-126">If you want to create a new group with a different name, you can use the [Azure Portal](https://portal.azure.com), and then close the page and restart to reload the list of resource groups.</span></span>
1. <span data-ttu-id="2595c-127">Choose the region in which to create the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2595c-127">Choose the region in which to create the Key Vault.</span></span> <span data-ttu-id="2595c-128">If your web application is hosted in Azure, choose the region that hosts the web application for optimum performance.</span><span class="sxs-lookup"><span data-stu-id="2595c-128">If your web application is hosted in Azure, choose the region that hosts the web application for optimum performance.</span></span>
1. <span data-ttu-id="2595c-129">Choose a pricing model.</span><span class="sxs-lookup"><span data-stu-id="2595c-129">Choose a pricing model.</span></span> <span data-ttu-id="2595c-130">For details, see [Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="2595c-130">For details, see [Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>
1. <span data-ttu-id="2595c-131">Choose OK to accept the configuration choices.</span><span class="sxs-lookup"><span data-stu-id="2595c-131">Choose OK to accept the configuration choices.</span></span>
1. <span data-ttu-id="2595c-132">Choose **Add** to create the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2595c-132">Choose **Add** to create the Key Vault.</span></span> <span data-ttu-id="2595c-133">The create process might fail if you choose a name that was already used.</span><span class="sxs-lookup"><span data-stu-id="2595c-133">The create process might fail if you choose a name that was already used.</span></span>  <span data-ttu-id="2595c-134">If that happens, use the **Edit** link to rename the Key Vault and try again.</span><span class="sxs-lookup"><span data-stu-id="2595c-134">If that happens, use the **Edit** link to rename the Key Vault and try again.</span></span>

   ![Adding connected service to project](media/vs-key-vault-add-connected-service/KeyVaultConnectedService4.PNG)

1. <span data-ttu-id="2595c-136">Now, add a secret in your Key Vault in Azure.</span><span class="sxs-lookup"><span data-stu-id="2595c-136">Now, add a secret in your Key Vault in Azure.</span></span> <span data-ttu-id="2595c-137">To get to the right place in the portal, click on the link for Manage secrets stored in this Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2595c-137">To get to the right place in the portal, click on the link for Manage secrets stored in this Key Vault.</span></span> <span data-ttu-id="2595c-138">If you closed the page or the project, you can navigate to it in the [Azure portal](https://portal.azure.com) by choosing **All Services**, under **Security**, choose **Key Vault**, then choose the Key Vault you just created.</span><span class="sxs-lookup"><span data-stu-id="2595c-138">If you closed the page or the project, you can navigate to it in the [Azure portal](https://portal.azure.com) by choosing **All Services**, under **Security**, choose **Key Vault**, then choose the Key Vault you just created.</span></span>

   ![Navigating to the portal](media/vs-key-vault-add-connected-service/manage-secrets-link.jpg)

1. <span data-ttu-id="2595c-140">In the Key Vault section for the key vault you created, choose **Secrets**, then **Generate/Import**.</span><span class="sxs-lookup"><span data-stu-id="2595c-140">In the Key Vault section for the key vault you created, choose **Secrets**, then **Generate/Import**.</span></span>

   ![Generate/Import a secret](media/vs-key-vault-add-connected-service/generate-secrets.jpg)

1. <span data-ttu-id="2595c-142">Enter a secret, such as "MySecret", and give it any string value as a test, then choose the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="2595c-142">Enter a secret, such as "MySecret", and give it any string value as a test, then choose the **Create** button.</span></span>

   ![Create a secret](media/vs-key-vault-add-connected-service/create-a-secret.jpg)

1. <span data-ttu-id="2595c-144">(optional) Enter another secret, but this time put it into a category by naming it "Secrets--MySecret".</span><span class="sxs-lookup"><span data-stu-id="2595c-144">(optional) Enter another secret, but this time put it into a category by naming it "Secrets--MySecret".</span></span> <span data-ttu-id="2595c-145">This syntax specifies a category "Secrets" that contains a secret "MySecret."</span><span class="sxs-lookup"><span data-stu-id="2595c-145">This syntax specifies a category "Secrets" that contains a secret "MySecret."</span></span>
 
<span data-ttu-id="2595c-146">Now, you can access your secrets in code.</span><span class="sxs-lookup"><span data-stu-id="2595c-146">Now, you can access your secrets in code.</span></span> <span data-ttu-id="2595c-147">The next steps are different depending on whether you are using ASP.NET 4.7.1 or ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2595c-147">The next steps are different depending on whether you are using ASP.NET 4.7.1 or ASP.NET Core.</span></span>

## <a name="access-your-secrets-in-code-aspnet-core-projects"></a><span data-ttu-id="2595c-148">Access your secrets in code (ASP.NET Core projects)</span><span class="sxs-lookup"><span data-stu-id="2595c-148">Access your secrets in code (ASP.NET Core projects)</span></span>

<span data-ttu-id="2595c-149">The connection to Key Vault is set up at startup by a class that implements [Microsoft.AspNetCore.Hosting.IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup?view=aspnetcore-2.1) using a way of extending startup behavior that is described in [Enhance an app from an external assembly in ASP.NET Core with IHostingStartup](/aspnet/core/fundamentals/host/platform-specific-configuration).</span><span class="sxs-lookup"><span data-stu-id="2595c-149">The connection to Key Vault is set up at startup by a class that implements [Microsoft.AspNetCore.Hosting.IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup?view=aspnetcore-2.1) using a way of extending startup behavior that is described in [Enhance an app from an external assembly in ASP.NET Core with IHostingStartup](/aspnet/core/fundamentals/host/platform-specific-configuration).</span></span> <span data-ttu-id="2595c-150">The startup class uses two environment variables that contain the Key Vault connection information: ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONENABLED, set to true, and ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONVAULT, set to your Key Vault URL.</span><span class="sxs-lookup"><span data-stu-id="2595c-150">The startup class uses two environment variables that contain the Key Vault connection information: ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONENABLED, set to true, and ASPNETCORE_HOSTINGSTARTUP__KEYVAULT__CONFIGURATIONVAULT, set to your Key Vault URL.</span></span> <span data-ttu-id="2595c-151">These are added to the launchsettings.json file when you run through the **Add Connected Service** process.</span><span class="sxs-lookup"><span data-stu-id="2595c-151">These are added to the launchsettings.json file when you run through the **Add Connected Service** process.</span></span>

<span data-ttu-id="2595c-152">To access your secrets:</span><span class="sxs-lookup"><span data-stu-id="2595c-152">To access your secrets:</span></span>

1. <span data-ttu-id="2595c-153">In Visual Studio, in your ASP.NET Core project, you can now reference these secrets by using the following expressions in code:</span><span class="sxs-lookup"><span data-stu-id="2595c-153">In Visual Studio, in your ASP.NET Core project, you can now reference these secrets by using the following expressions in code:</span></span>
 
   ```csharp
      config["MySecret"] // Access a secret without a section
      config["Secrets:MySecret"] // Access a secret in a section
      config.GetSection("Secrets")["MySecret"] // Get the configuration section and access a secret in it.
   ```

1. <span data-ttu-id="2595c-154">On a .cshtml page, say About.cshtml, add the @inject directive near the top of the file to set up a variable you can use to access the Key Vault configuration.</span><span class="sxs-lookup"><span data-stu-id="2595c-154">On a .cshtml page, say About.cshtml, add the @inject directive near the top of the file to set up a variable you can use to access the Key Vault configuration.</span></span>

   ```cshtml
      @inject Microsoft.Extensions.Configuration.IConfiguration config
   ```

1. <span data-ttu-id="2595c-155">As a test, you can confirm that the value of the secret is available by displaying it on one of the pages.</span><span class="sxs-lookup"><span data-stu-id="2595c-155">As a test, you can confirm that the value of the secret is available by displaying it on one of the pages.</span></span> <span data-ttu-id="2595c-156">Use @config to reference the config variable.</span><span class="sxs-lookup"><span data-stu-id="2595c-156">Use @config to reference the config variable.</span></span>
 
   ```cshtml
      <p> @config["MySecret"] </p>
      <p> @config.GetSection("Secrets")["MySecret"] </p>
      <p> @config["Secrets:MySecret"] </p>
   ```

1. <span data-ttu-id="2595c-157">Build and run the web application, navigate to the About page, and see the "secret" value.</span><span class="sxs-lookup"><span data-stu-id="2595c-157">Build and run the web application, navigate to the About page, and see the "secret" value.</span></span>

## <a name="access-your-secrets-in-code-aspnet-471-projects"></a><span data-ttu-id="2595c-158">Access your secrets in code (ASP.NET 4.7.1 projects)</span><span class="sxs-lookup"><span data-stu-id="2595c-158">Access your secrets in code (ASP.NET 4.7.1 projects)</span></span>

<span data-ttu-id="2595c-159">The connection to your Key Vault is set up by the ConfigurationBuilder class using information that was added to your web.config file when you run through the **Add Connected Service** process.</span><span class="sxs-lookup"><span data-stu-id="2595c-159">The connection to your Key Vault is set up by the ConfigurationBuilder class using information that was added to your web.config file when you run through the **Add Connected Service** process.</span></span>

<span data-ttu-id="2595c-160">To access your secrets:</span><span class="sxs-lookup"><span data-stu-id="2595c-160">To access your secrets:</span></span>

1. <span data-ttu-id="2595c-161">Modify web.config as follows.</span><span class="sxs-lookup"><span data-stu-id="2595c-161">Modify web.config as follows.</span></span> <span data-ttu-id="2595c-162">The keys are placeholders that will be replaced by the AzureKeyVault ConfigurationBuilder with the values of secrets in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2595c-162">The keys are placeholders that will be replaced by the AzureKeyVault ConfigurationBuilder with the values of secrets in Key Vault.</span></span>

   ```xml
     <appSettings configBuilders="AzureKeyVault">
       <add key="webpages:Version" value="3.0.0.0" />
       <add key="webpages:Enabled" value="false" />
       <add key="ClientValidationEnabled" value="true" />
       <add key="UnobtrusiveJavaScriptEnabled" value="true" />
       <add key="MySecret" value="dummy1"/>
       <add key="Secrets--MySecret" value="dummy2"/>
     </appSettings>
   ```

1. <span data-ttu-id="2595c-163">In the HomeController, in the About controller method, add the following lines to retrieve the secret and store it in the ViewBag.</span><span class="sxs-lookup"><span data-stu-id="2595c-163">In the HomeController, in the About controller method, add the following lines to retrieve the secret and store it in the ViewBag.</span></span>
 
   ```csharp
            var secret = ConfigurationManager.AppSettings["MySecret"];
            var secret2 = ConfigurationManager.AppSettings["Secrets--MySecret"];
            ViewBag.Secret = $"Secret: {secret}";
            ViewBag.Secret2 = $"Secret2: {secret2}";
   ```

1. <span data-ttu-id="2595c-164">In the About.cshtml view, add the following to display the value of the secret (for testing only).</span><span class="sxs-lookup"><span data-stu-id="2595c-164">In the About.cshtml view, add the following to display the value of the secret (for testing only).</span></span>

   ```csharp
      <h3>@ViewBag.Secret</h3>
      <h3>@ViewBag.Secret2</h3>
   ```

<span data-ttu-id="2595c-165">Congratulations, you have now confirmed that your web app can use Key Vault to access securely stored secrets.</span><span class="sxs-lookup"><span data-stu-id="2595c-165">Congratulations, you have now confirmed that your web app can use Key Vault to access securely stored secrets.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2595c-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2595c-166">Clean up resources</span></span>

<span data-ttu-id="2595c-167">When no longer needed, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="2595c-167">When no longer needed, delete the resource group.</span></span> <span data-ttu-id="2595c-168">This deletes the Key Vault and related resources.</span><span class="sxs-lookup"><span data-stu-id="2595c-168">This deletes the Key Vault and related resources.</span></span> <span data-ttu-id="2595c-169">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="2595c-169">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="2595c-170">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="2595c-170">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="2595c-171">When you see the resource group used in this QuickStart in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="2595c-171">When you see the resource group used in this QuickStart in the search results, select it.</span></span>
2. <span data-ttu-id="2595c-172">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="2595c-172">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="2595c-173">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2595c-173">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2595c-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="2595c-174">Next steps</span></span>

<span data-ttu-id="2595c-175">Learn more about Key Vault development by reading the [Key Vault Developer's Guide](key-vault-developers-guide.md)</span><span class="sxs-lookup"><span data-stu-id="2595c-175">Learn more about Key Vault development by reading the [Key Vault Developer's Guide](key-vault-developers-guide.md)</span></span>