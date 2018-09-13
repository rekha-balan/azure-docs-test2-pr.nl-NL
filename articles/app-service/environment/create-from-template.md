---
title: Create an Azure App Service environment by using a Resource Manager template
description: Explains how to create an External or ILB Azure App Service environment by using a Resource Manager template
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 92422a254bcfd5b31731dda6d1790cc85f467860
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871147"
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="072f8-103">Create an ASE by using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="072f8-103">Create an ASE by using an Azure Resource Manager template</span></span>

## <a name="overview"></a><span data-ttu-id="072f8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="072f8-104">Overview</span></span>
<span data-ttu-id="072f8-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span><span class="sxs-lookup"><span data-stu-id="072f8-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span></span> <span data-ttu-id="072f8-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span><span class="sxs-lookup"><span data-stu-id="072f8-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span></span> <span data-ttu-id="072f8-107">The ASE on an internal IP address is called an ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-107">The ASE on an internal IP address is called an ILB ASE.</span></span> <span data-ttu-id="072f8-108">The ASE with a public endpoint is called an External ASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-108">The ASE with a public endpoint is called an External ASE.</span></span> 

<span data-ttu-id="072f8-109">An ASE can be created by using the Azure portal or an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="072f8-109">An ASE can be created by using the Azure portal or an Azure Resource Manager template.</span></span> <span data-ttu-id="072f8-110">This article walks through the steps and syntax you need to create an External ASE or ILB ASE with Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="072f8-110">This article walks through the steps and syntax you need to create an External ASE or ILB ASE with Resource Manager templates.</span></span> <span data-ttu-id="072f8-111">To learn how to create an ASE in the Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="072f8-111">To learn how to create an ASE in the Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="072f8-112">When you create an ASE in the Azure portal, you can create your VNet at the same time or choose a preexisting VNet to deploy into.</span><span class="sxs-lookup"><span data-stu-id="072f8-112">When you create an ASE in the Azure portal, you can create your VNet at the same time or choose a preexisting VNet to deploy into.</span></span> <span data-ttu-id="072f8-113">When you create an ASE from a template, you must start with:</span><span class="sxs-lookup"><span data-stu-id="072f8-113">When you create an ASE from a template, you must start with:</span></span> 

* <span data-ttu-id="072f8-114">A Resource Manager VNet.</span><span class="sxs-lookup"><span data-stu-id="072f8-114">A Resource Manager VNet.</span></span>
* <span data-ttu-id="072f8-115">A subnet in that VNet.</span><span class="sxs-lookup"><span data-stu-id="072f8-115">A subnet in that VNet.</span></span> <span data-ttu-id="072f8-116">We recommend an ASE subnet size of `/24` with 256 addresses to accomodate future growth and scaling needs.</span><span class="sxs-lookup"><span data-stu-id="072f8-116">We recommend an ASE subnet size of `/24` with 256 addresses to accomodate future growth and scaling needs.</span></span> <span data-ttu-id="072f8-117">After the ASE is created, you can't change the size.</span><span class="sxs-lookup"><span data-stu-id="072f8-117">After the ASE is created, you can't change the size.</span></span>
* <span data-ttu-id="072f8-118">The resource ID from your VNet.</span><span class="sxs-lookup"><span data-stu-id="072f8-118">The resource ID from your VNet.</span></span> <span data-ttu-id="072f8-119">You can get this information from the Azure portal under your virtual network properties.</span><span class="sxs-lookup"><span data-stu-id="072f8-119">You can get this information from the Azure portal under your virtual network properties.</span></span>
* <span data-ttu-id="072f8-120">The subscription you want to deploy into.</span><span class="sxs-lookup"><span data-stu-id="072f8-120">The subscription you want to deploy into.</span></span>
* <span data-ttu-id="072f8-121">The location you want to deploy into.</span><span class="sxs-lookup"><span data-stu-id="072f8-121">The location you want to deploy into.</span></span>

<span data-ttu-id="072f8-122">To automate your ASE creation:</span><span class="sxs-lookup"><span data-stu-id="072f8-122">To automate your ASE creation:</span></span>

1. <span data-ttu-id="072f8-123">Create the ASE from a template.</span><span class="sxs-lookup"><span data-stu-id="072f8-123">Create the ASE from a template.</span></span> <span data-ttu-id="072f8-124">If you create an External ASE, you're finished after this step.</span><span class="sxs-lookup"><span data-stu-id="072f8-124">If you create an External ASE, you're finished after this step.</span></span> <span data-ttu-id="072f8-125">If you create an ILB ASE, there are a few more things to do.</span><span class="sxs-lookup"><span data-stu-id="072f8-125">If you create an ILB ASE, there are a few more things to do.</span></span>

2. <span data-ttu-id="072f8-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span><span class="sxs-lookup"><span data-stu-id="072f8-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span></span>

3. <span data-ttu-id="072f8-127">The uploaded SSL certificate is assigned to the ILB ASE as its "default" SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-127">The uploaded SSL certificate is assigned to the ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="072f8-128">This certificate is used for SSL traffic to apps on the ILB ASE when they use the common root domain that's assigned to the ASE (for example, https://someapp.mycustomrootdomain.com).</span><span class="sxs-lookup"><span data-stu-id="072f8-128">This certificate is used for SSL traffic to apps on the ILB ASE when they use the common root domain that's assigned to the ASE (for example, https://someapp.mycustomrootdomain.com).</span></span>


## <a name="create-the-ase"></a><span data-ttu-id="072f8-129">Create the ASE</span><span class="sxs-lookup"><span data-stu-id="072f8-129">Create the ASE</span></span>
<span data-ttu-id="072f8-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="072f8-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span></span>

<span data-ttu-id="072f8-131">If you want to make an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span><span class="sxs-lookup"><span data-stu-id="072f8-131">If you want to make an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span></span> <span data-ttu-id="072f8-132">They cater to that use case.</span><span class="sxs-lookup"><span data-stu-id="072f8-132">They cater to that use case.</span></span> <span data-ttu-id="072f8-133">Most of the parameters in the *azuredeploy.parameters.json* file are common to the creation of ILB ASEs and External ASEs.</span><span class="sxs-lookup"><span data-stu-id="072f8-133">Most of the parameters in the *azuredeploy.parameters.json* file are common to the creation of ILB ASEs and External ASEs.</span></span> <span data-ttu-id="072f8-134">The following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span><span class="sxs-lookup"><span data-stu-id="072f8-134">The following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span></span>

* <span data-ttu-id="072f8-135">*internalLoadBalancingMode*: In most cases, set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB-allocated virtual network internal address.</span><span class="sxs-lookup"><span data-stu-id="072f8-135">*internalLoadBalancingMode*: In most cases, set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB-allocated virtual network internal address.</span></span> <span data-ttu-id="072f8-136">If this property is set to 2, only the FTP service-related ports (both control and data channels) are bound to an ILB address.</span><span class="sxs-lookup"><span data-stu-id="072f8-136">If this property is set to 2, only the FTP service-related ports (both control and data channels) are bound to an ILB address.</span></span> <span data-ttu-id="072f8-137">The HTTP/HTTPS traffic remains on the public VIP.</span><span class="sxs-lookup"><span data-stu-id="072f8-137">The HTTP/HTTPS traffic remains on the public VIP.</span></span>
* <span data-ttu-id="072f8-138">*dnsSuffix*: This parameter defines the default root domain that's assigned to the ASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-138">*dnsSuffix*: This parameter defines the default root domain that's assigned to the ASE.</span></span> <span data-ttu-id="072f8-139">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="072f8-139">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span></span> <span data-ttu-id="072f8-140">Because an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span><span class="sxs-lookup"><span data-stu-id="072f8-140">Because an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span></span> <span data-ttu-id="072f8-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span><span class="sxs-lookup"><span data-stu-id="072f8-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span> <span data-ttu-id="072f8-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to be resolvable and accessible only within Contoso's virtual network.</span><span class="sxs-lookup"><span data-stu-id="072f8-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to be resolvable and accessible only within Contoso's virtual network.</span></span> 
* <span data-ttu-id="072f8-143">*ipSslAddressCount*: This parameter automatically defaults to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span><span class="sxs-lookup"><span data-stu-id="072f8-143">*ipSslAddressCount*: This parameter automatically defaults to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span> <span data-ttu-id="072f8-144">There are no explicit IP-SSL addresses for an ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-144">There are no explicit IP-SSL addresses for an ILB ASE.</span></span> <span data-ttu-id="072f8-145">Hence, the IP-SSL address pool for an ILB ASE must be set to zero.</span><span class="sxs-lookup"><span data-stu-id="072f8-145">Hence, the IP-SSL address pool for an ILB ASE must be set to zero.</span></span> <span data-ttu-id="072f8-146">Otherwise, a provisioning error occurs.</span><span class="sxs-lookup"><span data-stu-id="072f8-146">Otherwise, a provisioning error occurs.</span></span> 

<span data-ttu-id="072f8-147">After the *azuredeploy.parameters.json* file is filled in, create the ASE by using the PowerShell code snippet.</span><span class="sxs-lookup"><span data-stu-id="072f8-147">After the *azuredeploy.parameters.json* file is filled in, create the ASE by using the PowerShell code snippet.</span></span> <span data-ttu-id="072f8-148">Change the file paths to match the Resource Manager template-file locations on your machine.</span><span class="sxs-lookup"><span data-stu-id="072f8-148">Change the file paths to match the Resource Manager template-file locations on your machine.</span></span> <span data-ttu-id="072f8-149">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span><span class="sxs-lookup"><span data-stu-id="072f8-149">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

```powershell
$templatePath="PATH\azuredeploy.json"
$parameterPath="PATH\azuredeploy.parameters.json"

New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath
```

<span data-ttu-id="072f8-150">It takes about an hour for the ASE to be created.</span><span class="sxs-lookup"><span data-stu-id="072f8-150">It takes about an hour for the ASE to be created.</span></span> <span data-ttu-id="072f8-151">Then the ASE shows up in the portal in the list of ASEs for the subscription that triggered the deployment.</span><span class="sxs-lookup"><span data-stu-id="072f8-151">Then the ASE shows up in the portal in the list of ASEs for the subscription that triggered the deployment.</span></span>

## <a name="upload-and-configure-the-default-ssl-certificate"></a><span data-ttu-id="072f8-152">Upload and configure the "default" SSL certificate</span><span class="sxs-lookup"><span data-stu-id="072f8-152">Upload and configure the "default" SSL certificate</span></span>
<span data-ttu-id="072f8-153">An SSL certificate must be associated with the ASE as the "default" SSL certificate that's used to establish SSL connections to apps.</span><span class="sxs-lookup"><span data-stu-id="072f8-153">An SSL certificate must be associated with the ASE as the "default" SSL certificate that's used to establish SSL connections to apps.</span></span> <span data-ttu-id="072f8-154">If the ASE's default DNS suffix is *internal-contoso.com*, a connection to https://some-random-app.internal-contoso.com requires an SSL certificate that's valid for \**.internal-contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="072f8-154">If the ASE's default DNS suffix is *internal-contoso.com*, a connection to https://some-random-app.internal-contoso.com requires an SSL certificate that's valid for \**.internal-contoso.com*.</span></span> 

<span data-ttu-id="072f8-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span></span> <span data-ttu-id="072f8-156">Regardless of the source of the SSL certificate, the following certificate attributes must be configured properly:</span><span class="sxs-lookup"><span data-stu-id="072f8-156">Regardless of the source of the SSL certificate, the following certificate attributes must be configured properly:</span></span>

* <span data-ttu-id="072f8-157">**Subject**: This attribute must be set to \**.your-root-domain-here.com*.</span><span class="sxs-lookup"><span data-stu-id="072f8-157">**Subject**: This attribute must be set to \**.your-root-domain-here.com*.</span></span>
* <span data-ttu-id="072f8-158">**Subject Alternative Name**: This attribute must include both \**.your-root-domain-here.com* and \**.scm.your-root-domain-here.com*.</span><span class="sxs-lookup"><span data-stu-id="072f8-158">**Subject Alternative Name**: This attribute must include both \**.your-root-domain-here.com* and \**.scm.your-root-domain-here.com*.</span></span> <span data-ttu-id="072f8-159">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here.com*.</span><span class="sxs-lookup"><span data-stu-id="072f8-159">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="072f8-160">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span><span class="sxs-lookup"><span data-stu-id="072f8-160">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span> <span data-ttu-id="072f8-161">Convert/save the SSL certificate as a .pfx file.</span><span class="sxs-lookup"><span data-stu-id="072f8-161">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="072f8-162">Remember that the .pfx file must include all intermediate and root certificates.</span><span class="sxs-lookup"><span data-stu-id="072f8-162">Remember that the .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="072f8-163">Secure it with a password.</span><span class="sxs-lookup"><span data-stu-id="072f8-163">Secure it with a password.</span></span>

<span data-ttu-id="072f8-164">The .pfx file needs to be converted into a base64 string because the SSL certificate is uploaded by using a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="072f8-164">The .pfx file needs to be converted into a base64 string because the SSL certificate is uploaded by using a Resource Manager template.</span></span> <span data-ttu-id="072f8-165">Because Resource Manager templates are text files, the .pfx file must be converted into a base64 string.</span><span class="sxs-lookup"><span data-stu-id="072f8-165">Because Resource Manager templates are text files, the .pfx file must be converted into a base64 string.</span></span> <span data-ttu-id="072f8-166">This way it can be included as a parameter of the template.</span><span class="sxs-lookup"><span data-stu-id="072f8-166">This way it can be included as a parameter of the template.</span></span>

<span data-ttu-id="072f8-167">Use the following PowerShell code snippet to:</span><span class="sxs-lookup"><span data-stu-id="072f8-167">Use the following PowerShell code snippet to:</span></span>

* <span data-ttu-id="072f8-168">Generate a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-168">Generate a self-signed certificate.</span></span>
* <span data-ttu-id="072f8-169">Export the certificate as a .pfx file.</span><span class="sxs-lookup"><span data-stu-id="072f8-169">Export the certificate as a .pfx file.</span></span>
* <span data-ttu-id="072f8-170">Convert the .pfx file into a base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="072f8-170">Convert the .pfx file into a base64-encoded string.</span></span>
* <span data-ttu-id="072f8-171">Save the base64-encoded string to a separate file.</span><span class="sxs-lookup"><span data-stu-id="072f8-171">Save the base64-encoded string to a separate file.</span></span> 

<span data-ttu-id="072f8-172">This PowerShell code for base64 encoding was adapted from the [PowerShell scripts blog][examplebase64encoding]:</span><span class="sxs-lookup"><span data-stu-id="072f8-172">This PowerShell code for base64 encoding was adapted from the [PowerShell scripts blog][examplebase64encoding]:</span></span>

```powershell
$certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

$certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
$password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

$fileName = "exportedcert.pfx"
Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

$fileContentBytes = get-content -encoding byte $fileName
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$fileContentEncoded | set-content ($fileName + ".b64")
```

<span data-ttu-id="072f8-173">After the SSL certificate is successfully generated and converted to a base64-encoded string, use the example Resource Manager template [Configure the default SSL certificate][quickstartconfiguressl] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="072f8-173">After the SSL certificate is successfully generated and converted to a base64-encoded string, use the example Resource Manager template [Configure the default SSL certificate][quickstartconfiguressl] on GitHub.</span></span> 

<span data-ttu-id="072f8-174">The parameters in the *azuredeploy.parameters.json* file are listed here:</span><span class="sxs-lookup"><span data-stu-id="072f8-174">The parameters in the *azuredeploy.parameters.json* file are listed here:</span></span>

* <span data-ttu-id="072f8-175">*appServiceEnvironmentName*: The name of the ILB ASE being configured.</span><span class="sxs-lookup"><span data-stu-id="072f8-175">*appServiceEnvironmentName*: The name of the ILB ASE being configured.</span></span>
* <span data-ttu-id="072f8-176">*existingAseLocation*: Text string containing the Azure region where the ILB ASE was deployed.</span><span class="sxs-lookup"><span data-stu-id="072f8-176">*existingAseLocation*: Text string containing the Azure region where the ILB ASE was deployed.</span></span>  <span data-ttu-id="072f8-177">For example: "South Central US".</span><span class="sxs-lookup"><span data-stu-id="072f8-177">For example: "South Central US".</span></span>
* <span data-ttu-id="072f8-178">*pfxBlobString*: The based64-encoded string representation of the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="072f8-178">*pfxBlobString*: The based64-encoded string representation of the .pfx file.</span></span> <span data-ttu-id="072f8-179">Use the code snippet shown earlier and copy the string contained in "exportedcert.pfx.b64".</span><span class="sxs-lookup"><span data-stu-id="072f8-179">Use the code snippet shown earlier and copy the string contained in "exportedcert.pfx.b64".</span></span> <span data-ttu-id="072f8-180">Paste it in as the value of the *pfxBlobString* attribute.</span><span class="sxs-lookup"><span data-stu-id="072f8-180">Paste it in as the value of the *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="072f8-181">*password*: The password used to secure the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="072f8-181">*password*: The password used to secure the .pfx file.</span></span>
* <span data-ttu-id="072f8-182">*certificateThumbprint*: The certificate's thumbprint.</span><span class="sxs-lookup"><span data-stu-id="072f8-182">*certificateThumbprint*: The certificate's thumbprint.</span></span> <span data-ttu-id="072f8-183">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from the earlier code snippet), you can use the value as is.</span><span class="sxs-lookup"><span data-stu-id="072f8-183">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from the earlier code snippet), you can use the value as is.</span></span> <span data-ttu-id="072f8-184">If you copy the value from the Windows certificate dialog box, remember to strip out the extraneous spaces.</span><span class="sxs-lookup"><span data-stu-id="072f8-184">If you copy the value from the Windows certificate dialog box, remember to strip out the extraneous spaces.</span></span> <span data-ttu-id="072f8-185">The *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span><span class="sxs-lookup"><span data-stu-id="072f8-185">The *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span></span>
* <span data-ttu-id="072f8-186">*certificateName*: A friendly string identifier of your own choosing used to identity the certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-186">*certificateName*: A friendly string identifier of your own choosing used to identity the certificate.</span></span> <span data-ttu-id="072f8-187">The name is used as part of the unique Resource Manager identifier for the *Microsoft.Web/certificates* entity that represents the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-187">The name is used as part of the unique Resource Manager identifier for the *Microsoft.Web/certificates* entity that represents the SSL certificate.</span></span> <span data-ttu-id="072f8-188">The name *must* end with the following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-188">The name *must* end with the following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span></span> <span data-ttu-id="072f8-189">The Azure portal uses this suffix as an indicator that the certificate is used to secure an ILB-enabled ASE.</span><span class="sxs-lookup"><span data-stu-id="072f8-189">The Azure portal uses this suffix as an indicator that the certificate is used to secure an ILB-enabled ASE.</span></span>

<span data-ttu-id="072f8-190">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span><span class="sxs-lookup"><span data-stu-id="072f8-190">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "appServiceEnvironmentName": {
      "value": "yourASENameHere"
    },
    "existingAseLocation": {
      "value": "East US 2"
    },
    "pfxBlobString": {
      "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
    },
    "password": {
      "value": "PASSWORDGOESHERE"
    },
    "certificateThumbprint": {
      "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
    },
    "certificateName": {
      "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
    }
  }
}
```

<span data-ttu-id="072f8-191">After the *azuredeploy.parameters.json* file is filled in, configure the default SSL certificate by using the PowerShell code snippet.</span><span class="sxs-lookup"><span data-stu-id="072f8-191">After the *azuredeploy.parameters.json* file is filled in, configure the default SSL certificate by using the PowerShell code snippet.</span></span> <span data-ttu-id="072f8-192">Change the file paths to match where the Resource Manager template files are located on your machine.</span><span class="sxs-lookup"><span data-stu-id="072f8-192">Change the file paths to match where the Resource Manager template files are located on your machine.</span></span> <span data-ttu-id="072f8-193">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span><span class="sxs-lookup"><span data-stu-id="072f8-193">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

```powershell
$templatePath="PATH\azuredeploy.json"
$parameterPath="PATH\azuredeploy.parameters.json"

New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath
```

<span data-ttu-id="072f8-194">It takes roughly 40 minutes per ASE front end to apply the change.</span><span class="sxs-lookup"><span data-stu-id="072f8-194">It takes roughly 40 minutes per ASE front end to apply the change.</span></span> <span data-ttu-id="072f8-195">For example, for a default-sized ASE that uses two front ends, the template takes around one hour and 20 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="072f8-195">For example, for a default-sized ASE that uses two front ends, the template takes around one hour and 20 minutes to complete.</span></span> <span data-ttu-id="072f8-196">While the template is running, the ASE can't scale.</span><span class="sxs-lookup"><span data-stu-id="072f8-196">While the template is running, the ASE can't scale.</span></span>  

<span data-ttu-id="072f8-197">After the template finishes, apps on the ILB ASE can be accessed over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="072f8-197">After the template finishes, apps on the ILB ASE can be accessed over HTTPS.</span></span> <span data-ttu-id="072f8-198">The connections are secured by using the default SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="072f8-198">The connections are secured by using the default SSL certificate.</span></span> <span data-ttu-id="072f8-199">The default SSL certificate is used when apps on the ILB ASE are addressed by using a combination of the application name plus the default host name.</span><span class="sxs-lookup"><span data-stu-id="072f8-199">The default SSL certificate is used when apps on the ILB ASE are addressed by using a combination of the application name plus the default host name.</span></span> <span data-ttu-id="072f8-200">For example, https://mycustomapp.internal-contoso.com uses the default SSL certificate for \**.internal-contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="072f8-200">For example, https://mycustomapp.internal-contoso.com uses the default SSL certificate for \**.internal-contoso.com*.</span></span>

<span data-ttu-id="072f8-201">However, just like apps that run on the public multitenant service, developers can configure custom host names for individual apps.</span><span class="sxs-lookup"><span data-stu-id="072f8-201">However, just like apps that run on the public multitenant service, developers can configure custom host names for individual apps.</span></span> <span data-ttu-id="072f8-202">They also can configure unique SNI SSL certificate bindings for individual apps.</span><span class="sxs-lookup"><span data-stu-id="072f8-202">They also can configure unique SNI SSL certificate bindings for individual apps.</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="072f8-203">App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="072f8-203">App Service Environment v1</span></span> ##
<span data-ttu-id="072f8-204">App Service Environment has two versions: ASEv1 and ASEv2.</span><span class="sxs-lookup"><span data-stu-id="072f8-204">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="072f8-205">The preceding information was based on ASEv2.</span><span class="sxs-lookup"><span data-stu-id="072f8-205">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="072f8-206">This section shows you the differences between ASEv1 and ASEv2.</span><span class="sxs-lookup"><span data-stu-id="072f8-206">This section shows you the differences between ASEv1 and ASEv2.</span></span>

<span data-ttu-id="072f8-207">In ASEv1, you manage all of the resources manually.</span><span class="sxs-lookup"><span data-stu-id="072f8-207">In ASEv1, you manage all of the resources manually.</span></span> <span data-ttu-id="072f8-208">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span><span class="sxs-lookup"><span data-stu-id="072f8-208">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="072f8-209">Before you can scale out your App Service plan, you must scale out the worker pool that you want to host it.</span><span class="sxs-lookup"><span data-stu-id="072f8-209">Before you can scale out your App Service plan, you must scale out the worker pool that you want to host it.</span></span>

<span data-ttu-id="072f8-210">ASEv1 uses a different pricing model from ASEv2.</span><span class="sxs-lookup"><span data-stu-id="072f8-210">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="072f8-211">In ASEv1, you pay for each vCPU allocated.</span><span class="sxs-lookup"><span data-stu-id="072f8-211">In ASEv1, you pay for each vCPU allocated.</span></span> <span data-ttu-id="072f8-212">That includes vCPUs that are used for front ends or workers that aren't hosting any workloads.</span><span class="sxs-lookup"><span data-stu-id="072f8-212">That includes vCPUs that are used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="072f8-213">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span><span class="sxs-lookup"><span data-stu-id="072f8-213">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="072f8-214">That includes workers and front ends.</span><span class="sxs-lookup"><span data-stu-id="072f8-214">That includes workers and front ends.</span></span> <span data-ttu-id="072f8-215">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span><span class="sxs-lookup"><span data-stu-id="072f8-215">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="072f8-216">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span><span class="sxs-lookup"><span data-stu-id="072f8-216">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<span data-ttu-id="072f8-217">To create an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span><span class="sxs-lookup"><span data-stu-id="072f8-217">To create an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span></span>


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/security-overview.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: app-service-app-service-environment-create-ilb-ase-resourcemanager.md
