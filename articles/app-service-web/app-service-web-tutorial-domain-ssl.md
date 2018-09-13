---
title: Add custom domain and SSL to an Azure web app | Microsoft Docs
description: Learn how to prepare your Azure web app to go production by adding your company branding. Map the custom domain name (vanity domain) to your web app and secure it with a custom SSL certificate.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/29/2017
ms.author: cephalin
ms.openlocfilehash: 0f019b4f3edb3c71db03433c76d7899a56e5ce8c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555873"
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="f6689-104">Add custom domain and SSL to an Azure web app</span><span class="sxs-lookup"><span data-stu-id="f6689-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="f6689-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="f6689-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f6689-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f6689-106">Before you begin</span></span>

<span data-ttu-id="f6689-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span><span class="sxs-lookup"><span data-stu-id="f6689-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="f6689-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span><span class="sxs-lookup"><span data-stu-id="f6689-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="f6689-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="f6689-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="f6689-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span><span class="sxs-lookup"><span data-stu-id="f6689-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="f6689-111">This SSL certificate should be configured to secure the custom domain name you want.</span><span class="sxs-lookup"><span data-stu-id="f6689-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="f6689-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="f6689-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="f6689-113">Step 1 - Create an Azure web app</span><span class="sxs-lookup"><span data-stu-id="f6689-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f6689-114">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f6689-114">Log in to Azure</span></span>

<span data-ttu-id="f6689-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6689-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="f6689-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="f6689-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="f6689-117">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f6689-117">Create a resource group</span></span>   
<span data-ttu-id="f6689-118">Create a resource group with the [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f6689-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f6689-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f6689-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="f6689-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="f6689-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="f6689-121">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="f6689-121">Create an App Service plan</span></span>

<span data-ttu-id="f6689-122">Create a Linux-based App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span><span class="sxs-lookup"><span data-stu-id="f6689-122">Create a Linux-based App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f6689-123">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="f6689-123">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="f6689-124">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="f6689-124">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span> 
> 
> <span data-ttu-id="f6689-125">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="f6689-125">App Service plans define:</span></span> 
> * <span data-ttu-id="f6689-126">Region (North Europe, East US, Southeast Asia)</span><span class="sxs-lookup"><span data-stu-id="f6689-126">Region (North Europe, East US, Southeast Asia)</span></span> 
> * <span data-ttu-id="f6689-127">Instance Size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="f6689-127">Instance Size (Small, Medium, Large)</span></span> 
> * <span data-ttu-id="f6689-128">Scale Count (one, two or three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="f6689-128">Scale Count (one, two or three instances, etc.)</span></span> 
> * <span data-ttu-id="f6689-129">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="f6689-129">SKU (Free, Shared, Basic, Standard, Premium)</span></span> 
> 

<span data-ttu-id="f6689-130">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f6689-130">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="f6689-131">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="f6689-131">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="f6689-132">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f6689-132">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="f6689-133">Create a web app</span><span class="sxs-lookup"><span data-stu-id="f6689-133">Create a web app</span></span>

<span data-ttu-id="f6689-134">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f6689-134">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="f6689-135">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span><span class="sxs-lookup"><span data-stu-id="f6689-135">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="f6689-136">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span><span class="sxs-lookup"><span data-stu-id="f6689-136">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="f6689-137">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="f6689-137">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="f6689-138">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6689-138">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="f6689-139">You can later map any custom DNS entry to the web app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="f6689-139">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="f6689-140">When the web app has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f6689-140">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="f6689-141">From the JSON output, `defaultHostName` shows your web app's default domain name.</span><span class="sxs-lookup"><span data-stu-id="f6689-141">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="f6689-142">In your browser, navigate to this address.</span><span class="sxs-lookup"><span data-stu-id="f6689-142">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="f6689-144">Step 2 - Configure DNS mapping</span><span class="sxs-lookup"><span data-stu-id="f6689-144">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="f6689-145">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f6689-145">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="f6689-146">Typically, you perform this step in your domain provider's website.</span><span class="sxs-lookup"><span data-stu-id="f6689-146">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="f6689-147">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span><span class="sxs-lookup"><span data-stu-id="f6689-147">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="f6689-148">However, here are some general guidelines.</span><span class="sxs-lookup"><span data-stu-id="f6689-148">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="f6689-149">Navigate to to DNS management page</span><span class="sxs-lookup"><span data-stu-id="f6689-149">Navigate to to DNS management page</span></span>

<span data-ttu-id="f6689-150">First, log in to your domain registrar's website.</span><span class="sxs-lookup"><span data-stu-id="f6689-150">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="f6689-151">Then, find the page for managing DNS records.</span><span class="sxs-lookup"><span data-stu-id="f6689-151">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="f6689-152">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="f6689-152">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="f6689-153">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span><span class="sxs-lookup"><span data-stu-id="f6689-153">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="f6689-154">Once you find this page, look for a link that lets you add or edit DNS records.</span><span class="sxs-lookup"><span data-stu-id="f6689-154">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="f6689-155">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span><span class="sxs-lookup"><span data-stu-id="f6689-155">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="f6689-156">Create a CNAME record</span><span class="sxs-lookup"><span data-stu-id="f6689-156">Create a CNAME record</span></span>

<span data-ttu-id="f6689-157">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span><span class="sxs-lookup"><span data-stu-id="f6689-157">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="f6689-158">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f6689-158">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="f6689-159">Step 3 - Configure the custom domain on your web app</span><span class="sxs-lookup"><span data-stu-id="f6689-159">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="f6689-160">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span><span class="sxs-lookup"><span data-stu-id="f6689-160">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="f6689-161">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span><span class="sxs-lookup"><span data-stu-id="f6689-161">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="f6689-162">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="f6689-162">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="f6689-163">The custom domain now is fully mapped to your web app.</span><span class="sxs-lookup"><span data-stu-id="f6689-163">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="f6689-164">In your browser, navigate to the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="f6689-164">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="f6689-165">For example:</span><span class="sxs-lookup"><span data-stu-id="f6689-165">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="f6689-167">Step 4 - Bind a custom SSL certificate to your web app</span><span class="sxs-lookup"><span data-stu-id="f6689-167">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="f6689-168">You now have an Azure web app, with the domain name you want in the browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="f6689-168">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="f6689-169">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span><span class="sxs-lookup"><span data-stu-id="f6689-169">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="f6689-171">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span><span class="sxs-lookup"><span data-stu-id="f6689-171">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="f6689-172">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f6689-172">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="f6689-173">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span><span class="sxs-lookup"><span data-stu-id="f6689-173">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="f6689-174">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span><span class="sxs-lookup"><span data-stu-id="f6689-174">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="f6689-175">You will do it in this step.</span><span class="sxs-lookup"><span data-stu-id="f6689-175">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="f6689-176">Upload the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f6689-176">Upload the SSL certificate</span></span>

<span data-ttu-id="f6689-177">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span><span class="sxs-lookup"><span data-stu-id="f6689-177">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="f6689-178">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span><span class="sxs-lookup"><span data-stu-id="f6689-178">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="f6689-179">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="f6689-179">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="f6689-180">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span><span class="sxs-lookup"><span data-stu-id="f6689-180">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="f6689-181">Copy its value for the next step.</span><span class="sxs-lookup"><span data-stu-id="f6689-181">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="f6689-182">Bind the uploaded SSL certificate to the web app</span><span class="sxs-lookup"><span data-stu-id="f6689-182">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="f6689-183">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span><span class="sxs-lookup"><span data-stu-id="f6689-183">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="f6689-184">The only thing left to do is to bind the uploaded certificate to the web app.</span><span class="sxs-lookup"><span data-stu-id="f6689-184">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="f6689-185">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span><span class="sxs-lookup"><span data-stu-id="f6689-185">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="f6689-186">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span><span class="sxs-lookup"><span data-stu-id="f6689-186">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="f6689-187">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="f6689-187">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="f6689-188">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="f6689-188">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="f6689-189">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="f6689-189">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="f6689-190">In your browser, navigate to HTTPS endpoint of your custom domain name.</span><span class="sxs-lookup"><span data-stu-id="f6689-190">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="f6689-191">For example:</span><span class="sxs-lookup"><span data-stu-id="f6689-191">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="f6689-193">More resources</span><span class="sxs-lookup"><span data-stu-id="f6689-193">More resources</span></span>

<span data-ttu-id="f6689-194">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="f6689-194">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>




