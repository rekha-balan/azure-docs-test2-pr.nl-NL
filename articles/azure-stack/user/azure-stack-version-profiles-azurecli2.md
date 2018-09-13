---
title: Connect to Azure Stack with CLI | Microsoft Docs
description: Learn how to use the cross-platform command-line interface (CLI) to manage and deploy resources on Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2018
ms.author: sethm
ms.reviewer: sijuman
ms.openlocfilehash: ec3b1f43c7b89a545ee5bb26c4cc0d068a993021
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857756"
---
# <a name="use-api-version-profiles-with-azure-cli-20-in-azure-stack"></a><span data-ttu-id="5b582-103">Use API version profiles with Azure CLI 2.0 in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5b582-103">Use API version profiles with Azure CLI 2.0 in Azure Stack</span></span>

<span data-ttu-id="5b582-104">You can follow the steps in this article to set up the Azure Command-Line Interface (CLI) to manage Azure Stack Development Kit resources from Linux, Mac, and Windows client platforms.</span><span class="sxs-lookup"><span data-stu-id="5b582-104">You can follow the steps in this article to set up the Azure Command-Line Interface (CLI) to manage Azure Stack Development Kit resources from Linux, Mac, and Windows client platforms.</span></span>

## <a name="install-cli"></a><span data-ttu-id="5b582-105">Install CLI</span><span class="sxs-lookup"><span data-stu-id="5b582-105">Install CLI</span></span>

<span data-ttu-id="5b582-106">Sign in to your development workstation and install CLI.</span><span class="sxs-lookup"><span data-stu-id="5b582-106">Sign in to your development workstation and install CLI.</span></span> <span data-ttu-id="5b582-107">Azure Stack requires the 2.0 version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5b582-107">Azure Stack requires the 2.0 version of Azure CLI.</span></span> <span data-ttu-id="5b582-108">You can install that by using the steps described in the [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) article.</span><span class="sxs-lookup"><span data-stu-id="5b582-108">You can install that by using the steps described in the [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) article.</span></span> <span data-ttu-id="5b582-109">To verify if the installation was successful, open a terminal or a command prompt window and run the following command:</span><span class="sxs-lookup"><span data-stu-id="5b582-109">To verify if the installation was successful, open a terminal or a command prompt window and run the following command:</span></span>

```azurecli
az --version
```

<span data-ttu-id="5b582-110">You should see the version of Azure CLI and other dependent libraries that are installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="5b582-110">You should see the version of Azure CLI and other dependent libraries that are installed on your computer.</span></span>

## <a name="trust-the-azure-stack-ca-root-certificate"></a><span data-ttu-id="5b582-111">Trust the Azure Stack CA root certificate</span><span class="sxs-lookup"><span data-stu-id="5b582-111">Trust the Azure Stack CA root certificate</span></span>

1. <span data-ttu-id="5b582-112">Get the Azure Stack CA root certificate from [your Azure Stack operator](..\azure-stack-cli-admin.md#export-the-azure-stack-ca-root-certificate) and trust it.</span><span class="sxs-lookup"><span data-stu-id="5b582-112">Get the Azure Stack CA root certificate from [your Azure Stack operator](..\azure-stack-cli-admin.md#export-the-azure-stack-ca-root-certificate) and trust it.</span></span> <span data-ttu-id="5b582-113">To trust the Azure Stack CA root certificate, append it to the existing Python certificate.</span><span class="sxs-lookup"><span data-stu-id="5b582-113">To trust the Azure Stack CA root certificate, append it to the existing Python certificate.</span></span>

1. <span data-ttu-id="5b582-114">Find the certificate location on your machine.</span><span class="sxs-lookup"><span data-stu-id="5b582-114">Find the certificate location on your machine.</span></span> <span data-ttu-id="5b582-115">The location may vary depending on where you have installed Python.</span><span class="sxs-lookup"><span data-stu-id="5b582-115">The location may vary depending on where you have installed Python.</span></span> <span data-ttu-id="5b582-116">You will need to have [pip](https://pip.pypa.io) and the [certifi](https://pypi.org/project/certifi/) module installed.</span><span class="sxs-lookup"><span data-stu-id="5b582-116">You will need to have [pip](https://pip.pypa.io) and the [certifi](https://pypi.org/project/certifi/) module installed.</span></span> <span data-ttu-id="5b582-117">You can use the following Python command from the bash prompt:</span><span class="sxs-lookup"><span data-stu-id="5b582-117">You can use the following Python command from the bash prompt:</span></span>

  ```bash  
    python -c "import certifi; print(certifi.where())"
  ```

  <span data-ttu-id="5b582-118">Make a note of the certificate location.</span><span class="sxs-lookup"><span data-stu-id="5b582-118">Make a note of the certificate location.</span></span> <span data-ttu-id="5b582-119">For example, `~/lib/python3.5/site-packages/certifi/cacert.pem`.</span><span class="sxs-lookup"><span data-stu-id="5b582-119">For example, `~/lib/python3.5/site-packages/certifi/cacert.pem`.</span></span> <span data-ttu-id="5b582-120">Your particular path will depend on your OS and the version of Python that you have installed.</span><span class="sxs-lookup"><span data-stu-id="5b582-120">Your particular path will depend on your OS and the version of Python that you have installed.</span></span>

### <a name="set-the-path-for-a-development-machine-inside-the-cloud"></a><span data-ttu-id="5b582-121">Set the path for a development machine inside the cloud</span><span class="sxs-lookup"><span data-stu-id="5b582-121">Set the path for a development machine inside the cloud</span></span>

<span data-ttu-id="5b582-122">If you are running CLI from a Linux machine that is created within the Azure Stack environment, run the following bash command with the path to your certificate.</span><span class="sxs-lookup"><span data-stu-id="5b582-122">If you are running CLI from a Linux machine that is created within the Azure Stack environment, run the following bash command with the path to your certificate.</span></span>

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/<yourpath>/cacert.pem
```

### <a name="set-the-path-for-a-development-machine-outside-the-cloud"></a><span data-ttu-id="5b582-123">Set the path for a development machine outside the cloud</span><span class="sxs-lookup"><span data-stu-id="5b582-123">Set the path for a development machine outside the cloud</span></span>

<span data-ttu-id="5b582-124">If you are running CLI from a machine **outside** the Azure Stack environment:</span><span class="sxs-lookup"><span data-stu-id="5b582-124">If you are running CLI from a machine **outside** the Azure Stack environment:</span></span>  

1. <span data-ttu-id="5b582-125">You must set up [VPN connectivity to Azure Stack](azure-stack-connect-azure-stack.md).</span><span class="sxs-lookup"><span data-stu-id="5b582-125">You must set up [VPN connectivity to Azure Stack](azure-stack-connect-azure-stack.md).</span></span>

1. <span data-ttu-id="5b582-126">Copy the PEM certificate that you got from Azure Stack operator, and make a note of the location of the file (PATH_TO_PEM_FILE).</span><span class="sxs-lookup"><span data-stu-id="5b582-126">Copy the PEM certificate that you got from Azure Stack operator, and make a note of the location of the file (PATH_TO_PEM_FILE).</span></span>

1. <span data-ttu-id="5b582-127">Run the following commands, depending ending on your development workstation's OS.</span><span class="sxs-lookup"><span data-stu-id="5b582-127">Run the following commands, depending ending on your development workstation's OS.</span></span>

#### <a name="linux"></a><span data-ttu-id="5b582-128">Linux</span><span class="sxs-lookup"><span data-stu-id="5b582-128">Linux</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/<yourpath>/cacert.pem
```

#### <a name="macos"></a><span data-ttu-id="5b582-129">macOS</span><span class="sxs-lookup"><span data-stu-id="5b582-129">macOS</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/<yourpath>/cacert.pem
```

#### <a name="windows"></a><span data-ttu-id="5b582-130">Windows</span><span class="sxs-lookup"><span data-stu-id="5b582-130">Windows</span></span>

```powershell
$pemFile = "<Fully qualified path to the PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from the cert file"
$md5Hash    = (Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash   = (Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash = (Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry  = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry   = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry  = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry     = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry    = [string]::Format("# SHA1 Fingerprint: {0}", $sha1Hash)
$sha256Entry  = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path $pemFile -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding the certificate content to Python Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing the azure stack CA root certificate"
```

## <a name="get-the-virtual-machine-aliases-endpoint"></a><span data-ttu-id="5b582-131">Get the virtual machine aliases endpoint</span><span class="sxs-lookup"><span data-stu-id="5b582-131">Get the virtual machine aliases endpoint</span></span>

<span data-ttu-id="5b582-132">Before users can create virtual machines by using CLI, they must contact the Azure Stack operator and get the virtual machine aliases endpoint URI.</span><span class="sxs-lookup"><span data-stu-id="5b582-132">Before users can create virtual machines by using CLI, they must contact the Azure Stack operator and get the virtual machine aliases endpoint URI.</span></span> <span data-ttu-id="5b582-133">For example, Azure uses the following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span><span class="sxs-lookup"><span data-stu-id="5b582-133">For example, Azure uses the following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span></span> <span data-ttu-id="5b582-134">The cloud administrator should set up a similar endpoint for Azure Stack with the images that are available in the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="5b582-134">The cloud administrator should set up a similar endpoint for Azure Stack with the images that are available in the Azure Stack marketplace.</span></span> <span data-ttu-id="5b582-135">Users need pass the endpoint URI to the `endpoint-vm-image-alias-doc` parameter to the `az cloud register` command as shown in the next section.</span><span class="sxs-lookup"><span data-stu-id="5b582-135">Users need pass the endpoint URI to the `endpoint-vm-image-alias-doc` parameter to the `az cloud register` command as shown in the next section.</span></span> 
   

## <a name="connect-to-azure-stack"></a><span data-ttu-id="5b582-136">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5b582-136">Connect to Azure Stack</span></span>

<span data-ttu-id="5b582-137">Use the following steps to connect to Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="5b582-137">Use the following steps to connect to Azure Stack:</span></span>

1. <span data-ttu-id="5b582-138">Register your Azure Stack environment by running the `az cloud register` command.</span><span class="sxs-lookup"><span data-stu-id="5b582-138">Register your Azure Stack environment by running the `az cloud register` command.</span></span>
   
   <span data-ttu-id="5b582-139">a.</span><span class="sxs-lookup"><span data-stu-id="5b582-139">a.</span></span> <span data-ttu-id="5b582-140">To register the *cloud administrative* environment, use:</span><span class="sxs-lookup"><span data-stu-id="5b582-140">To register the *cloud administrative* environment, use:</span></span>

      ```azurecli
      az cloud register \ 
        -n AzureStackAdmin \ 
        --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

   <span data-ttu-id="5b582-141">b.</span><span class="sxs-lookup"><span data-stu-id="5b582-141">b.</span></span> <span data-ttu-id="5b582-142">To register the *user* environment, use:</span><span class="sxs-lookup"><span data-stu-id="5b582-142">To register the *user* environment, use:</span></span>

      ```azurecli
      az cloud register \ 
        -n AzureStackUser \ 
        --endpoint-resource-manager "https://management.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

1. <span data-ttu-id="5b582-143">Set the active environment by using the following commands.</span><span class="sxs-lookup"><span data-stu-id="5b582-143">Set the active environment by using the following commands.</span></span>

   <span data-ttu-id="5b582-144">a.</span><span class="sxs-lookup"><span data-stu-id="5b582-144">a.</span></span> <span data-ttu-id="5b582-145">For the *cloud administrative* environment, use:</span><span class="sxs-lookup"><span data-stu-id="5b582-145">For the *cloud administrative* environment, use:</span></span>

      ```azurecli
      az cloud set \
        -n AzureStackAdmin
      ```

   <span data-ttu-id="5b582-146">b.</span><span class="sxs-lookup"><span data-stu-id="5b582-146">b.</span></span> <span data-ttu-id="5b582-147">For the *user* environment, use:</span><span class="sxs-lookup"><span data-stu-id="5b582-147">For the *user* environment, use:</span></span>

      ```azurecli
      az cloud set \
        -n AzureStackUser
      ```

1. <span data-ttu-id="5b582-148">Update your environment configuration to use the Azure Stack specific API version profile.</span><span class="sxs-lookup"><span data-stu-id="5b582-148">Update your environment configuration to use the Azure Stack specific API version profile.</span></span> <span data-ttu-id="5b582-149">To update the configuration, run the following command:</span><span class="sxs-lookup"><span data-stu-id="5b582-149">To update the configuration, run the following command:</span></span>

   ```azurecli
   az cloud update \
     --profile 2018-03-01-hybrid
   ```

    >[!NOTE]  
    ><span data-ttu-id="5b582-150">If you are running a version of the Azure Stack before the 1808 build, you will to have to use the API version profile **2017-03-09-profile** rather than the API version profile **2018-03-01-hybrid**.</span><span class="sxs-lookup"><span data-stu-id="5b582-150">If you are running a version of the Azure Stack before the 1808 build, you will to have to use the API version profile **2017-03-09-profile** rather than the API version profile **2018-03-01-hybrid**.</span></span>

1. <span data-ttu-id="5b582-151">Sign in to your Azure Stack environment by using the `az login` command.</span><span class="sxs-lookup"><span data-stu-id="5b582-151">Sign in to your Azure Stack environment by using the `az login` command.</span></span> <span data-ttu-id="5b582-152">You can sign in to the Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="5b582-152">You can sign in to the Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects).</span></span> 

   * <span data-ttu-id="5b582-153">Sign in as a *user*: You can either specify the username and password directly within the `az login` command or authenticate by using a browser.</span><span class="sxs-lookup"><span data-stu-id="5b582-153">Sign in as a *user*: You can either specify the username and password directly within the `az login` command or authenticate by using a browser.</span></span> <span data-ttu-id="5b582-154">You have to do the latter if your account has multi-factor authentication enabled.</span><span class="sxs-lookup"><span data-stu-id="5b582-154">You have to do the latter if your account has multi-factor authentication enabled.</span></span>

      ```azurecli
      az login \
        -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
      ```

      > [!NOTE]
      > <span data-ttu-id="5b582-155">If your user account has multi-factor authentication enabled, you can use the `az login command` without providing the `-u` parameter.</span><span class="sxs-lookup"><span data-stu-id="5b582-155">If your user account has multi-factor authentication enabled, you can use the `az login command` without providing the `-u` parameter.</span></span> <span data-ttu-id="5b582-156">Running the command gives you a URL and a code that you must use to authenticate.</span><span class="sxs-lookup"><span data-stu-id="5b582-156">Running the command gives you a URL and a code that you must use to authenticate.</span></span>
   
   * <span data-ttu-id="5b582-157">Sign in as a *service principal*: Before you sign in, [create a service principal through the Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span><span class="sxs-lookup"><span data-stu-id="5b582-157">Sign in as a *service principal*: Before you sign in, [create a service principal through the Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span></span> <span data-ttu-id="5b582-158">Now, sign in by using the following command:</span><span class="sxs-lookup"><span data-stu-id="5b582-158">Now, sign in by using the following command:</span></span>

      ```azurecli
      az login \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
        --service-principal \
        -u <Application Id of the Service Principal> \
        -p <Key generated for the Service Principal>
      ```

## <a name="test-the-connectivity"></a><span data-ttu-id="5b582-159">Test the connectivity</span><span class="sxs-lookup"><span data-stu-id="5b582-159">Test the connectivity</span></span>

<span data-ttu-id="5b582-160">Now that we've got everything setup, let's use CLI to create resources within Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5b582-160">Now that we've got everything setup, let's use CLI to create resources within Azure Stack.</span></span> <span data-ttu-id="5b582-161">For example, you can create a resource group for an application and add a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b582-161">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="5b582-162">Use the following command to create a resource group named "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="5b582-162">Use the following command to create a resource group named "MyResourceGroup":</span></span>

```azurecli
az group create \
  -n MyResourceGroup -l local
```

<span data-ttu-id="5b582-163">If the resource group is created successfully, the previous command outputs the following properties of the newly created resource:</span><span class="sxs-lookup"><span data-stu-id="5b582-163">If the resource group is created successfully, the previous command outputs the following properties of the newly created resource:</span></span>

![Resource group create output](media/azure-stack-connect-cli/image1.png)

## <a name="known-issues"></a><span data-ttu-id="5b582-165">Known issues</span><span class="sxs-lookup"><span data-stu-id="5b582-165">Known issues</span></span>
<span data-ttu-id="5b582-166">There are some known issues that you must be aware of when using CLI in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="5b582-166">There are some known issues that you must be aware of when using CLI in Azure Stack:</span></span>

 - <span data-ttu-id="5b582-167">The CLI interactive mode i.e</span><span class="sxs-lookup"><span data-stu-id="5b582-167">The CLI interactive mode i.e</span></span> <span data-ttu-id="5b582-168">the `az interactive` command is not yet supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5b582-168">the `az interactive` command is not yet supported in Azure Stack.</span></span>
 - <span data-ttu-id="5b582-169">To get the list of virtual machine images available in Azure Stack, use the `az vm images list --all` command instead of the `az vm image list` command.</span><span class="sxs-lookup"><span data-stu-id="5b582-169">To get the list of virtual machine images available in Azure Stack, use the `az vm images list --all` command instead of the `az vm image list` command.</span></span> <span data-ttu-id="5b582-170">Specifying the `--all` option makes sure that response returns only the images that are available in your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="5b582-170">Specifying the `--all` option makes sure that response returns only the images that are available in your Azure Stack environment.</span></span>
 - <span data-ttu-id="5b582-171">Virtual machine image aliases that are available in Azure may not be applicable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5b582-171">Virtual machine image aliases that are available in Azure may not be applicable to Azure Stack.</span></span> <span data-ttu-id="5b582-172">When using virtual machine images, you must use the entire URN parameter (Canonical:UbuntuServer:14.04.3-LTS:1.0.0) instead of the image alias.</span><span class="sxs-lookup"><span data-stu-id="5b582-172">When using virtual machine images, you must use the entire URN parameter (Canonical:UbuntuServer:14.04.3-LTS:1.0.0) instead of the image alias.</span></span> <span data-ttu-id="5b582-173">This URN must match the image specifications as derived from the `az vm images list` command.</span><span class="sxs-lookup"><span data-stu-id="5b582-173">This URN must match the image specifications as derived from the `az vm images list` command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b582-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b582-174">Next steps</span></span>

[<span data-ttu-id="5b582-175">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5b582-175">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="5b582-176">Enable Azure CLI for Azure Stack users (Operator)</span><span class="sxs-lookup"><span data-stu-id="5b582-176">Enable Azure CLI for Azure Stack users (Operator)</span></span>](..\azure-stack-cli-admin.md)

[<span data-ttu-id="5b582-177">Manage user permissions</span><span class="sxs-lookup"><span data-stu-id="5b582-177">Manage user permissions</span></span>](azure-stack-manage-permissions.md)
