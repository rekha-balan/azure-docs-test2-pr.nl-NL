---
title: 'PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs'
services: data-lake-store,hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/14/2017
ms.author: nitinme
ms.openlocfilehash: a22872fa2d351d1ae1040b8a515aeb4522a91fc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550569"
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="beda6-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span><span class="sxs-lookup"><span data-stu-id="beda6-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [Using Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Using PowerShell (for default storage)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Using PowerShell (for additional storage)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Using Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="beda6-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span><span class="sxs-lookup"><span data-stu-id="beda6-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="beda6-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="beda6-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

<span data-ttu-id="beda6-109">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span><span class="sxs-lookup"><span data-stu-id="beda6-109">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="beda6-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="beda6-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="beda6-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="beda6-112">Using Data Lake Store for HDInsight cluster storage</span><span class="sxs-lookup"><span data-stu-id="beda6-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="beda6-113">Here are some important considerations for using HDInsight with Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="beda6-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="beda6-114">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, and 3.5.</span><span class="sxs-lookup"><span data-stu-id="beda6-114">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, and 3.5.</span></span>

* <span data-ttu-id="beda6-115">For HBase clusters (Windows and Linux), Data Lake Store is **not supported** as a storage option, for both default storage as well as additional storage.</span><span class="sxs-lookup"><span data-stu-id="beda6-115">For HBase clusters (Windows and Linux), Data Lake Store is **not supported** as a storage option, for both default storage as well as additional storage.</span></span>


<span data-ttu-id="beda6-116">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="beda6-116">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="beda6-117">Create an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-117">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="beda6-118">Set up authentication for role-based access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-118">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="beda6-119">Create HDInsight cluster with authentication to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-119">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="beda6-120">Run a test job on the cluster</span><span class="sxs-lookup"><span data-stu-id="beda6-120">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="beda6-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="beda6-121">Prerequisites</span></span>
<span data-ttu-id="beda6-122">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="beda6-122">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="beda6-123">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="beda6-123">**An Azure subscription**.</span></span> <span data-ttu-id="beda6-124">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="beda6-124">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="beda6-125">**Azure PowerShell 1.0 or greater**.</span><span class="sxs-lookup"><span data-stu-id="beda6-125">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="beda6-126">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="beda6-126">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="beda6-127">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="beda6-127">**Windows SDK**.</span></span> <span data-ttu-id="beda6-128">You can install it from [here](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="beda6-128">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="beda6-129">You use this to create a security certificate.</span><span class="sxs-lookup"><span data-stu-id="beda6-129">You use this to create a security certificate.</span></span>
* <span data-ttu-id="beda6-130">**Azure Active Directory Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="beda6-130">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="beda6-131">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="beda6-131">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="beda6-132">However, you must be an Azure AD administrator to be able to create a service principal.</span><span class="sxs-lookup"><span data-stu-id="beda6-132">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="beda6-133">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span><span class="sxs-lookup"><span data-stu-id="beda6-133">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="beda6-134">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span><span class="sxs-lookup"><span data-stu-id="beda6-134">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="beda6-135">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-135">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="beda6-136">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="beda6-136">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="beda6-137">Create an Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-137">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="beda6-138">Follow these steps to create a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-138">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="beda6-139">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span><span class="sxs-lookup"><span data-stu-id="beda6-139">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="beda6-140">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span><span class="sxs-lookup"><span data-stu-id="beda6-140">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subsrcription is not whitelisted for Azure Data Lake Store. Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).
   >
   >
2. <span data-ttu-id="beda6-143">An Azure Data Lake Store account is associated with an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="beda6-143">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="beda6-144">Start by creating an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="beda6-144">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="beda6-145">![Create an Azure Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="beda6-145">![Create an Azure Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="beda6-146">Create an Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="beda6-146">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="beda6-147">The account name you specify must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="beda6-147">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="beda6-148">![Create an Azure Data Lake account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="beda6-148">![Create an Azure Data Lake account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake account")</span></span>
4. <span data-ttu-id="beda6-149">Verify that the account is successfully created.</span><span class="sxs-lookup"><span data-stu-id="beda6-149">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="beda6-150">The output for this should be **True**.</span><span class="sxs-lookup"><span data-stu-id="beda6-150">The output for this should be **True**.</span></span>
5. <span data-ttu-id="beda6-151">Upload some sample data to Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="beda6-151">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="beda6-152">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-152">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="beda6-153">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="beda6-153">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="beda6-154">Set up authentication for role-based access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-154">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="beda6-155">Every Azure subscription is associated with an Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beda6-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="beda6-156">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beda6-156">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="beda6-157">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span><span class="sxs-lookup"><span data-stu-id="beda6-157">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="beda6-158">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="beda6-158">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="beda6-159">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beda6-159">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="beda6-160">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span><span class="sxs-lookup"><span data-stu-id="beda6-160">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="beda6-161">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="beda6-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="beda6-162">Create an application in Azure Active Directory and a Service Principal</span><span class="sxs-lookup"><span data-stu-id="beda6-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="beda6-163">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="beda6-163">Create a self-signed certificate</span></span>
<span data-ttu-id="beda6-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="beda6-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="beda6-165">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span><span class="sxs-lookup"><span data-stu-id="beda6-165">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="beda6-166">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span><span class="sxs-lookup"><span data-stu-id="beda6-166">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="beda6-167">Use the following commands.</span><span class="sxs-lookup"><span data-stu-id="beda6-167">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="beda6-168">You will be prompted to enter the private key password.</span><span class="sxs-lookup"><span data-stu-id="beda6-168">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="beda6-169">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span><span class="sxs-lookup"><span data-stu-id="beda6-169">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="beda6-170">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span><span class="sxs-lookup"><span data-stu-id="beda6-170">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="beda6-171">Run the following command.</span><span class="sxs-lookup"><span data-stu-id="beda6-171">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="beda6-172">When prompted enter the private key password you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="beda6-172">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="beda6-173">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="beda6-173">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="beda6-174">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span><span class="sxs-lookup"><span data-stu-id="beda6-174">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="beda6-175">Create an Azure Active Directory and a service principal</span><span class="sxs-lookup"><span data-stu-id="beda6-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="beda6-176">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span><span class="sxs-lookup"><span data-stu-id="beda6-176">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="beda6-177">Run the following commands to create an application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="beda6-177">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="beda6-178">Paste the following cmdlets in the PowerShell console window.</span><span class="sxs-lookup"><span data-stu-id="beda6-178">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="beda6-179">Make sure the value you specify for the **-DisplayName** property is unique.</span><span class="sxs-lookup"><span data-stu-id="beda6-179">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="beda6-180">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span><span class="sxs-lookup"><span data-stu-id="beda6-180">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="beda6-181">Create a service principal using the application ID.</span><span class="sxs-lookup"><span data-stu-id="beda6-181">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="beda6-182">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-182">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="beda6-183">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span><span class="sxs-lookup"><span data-stu-id="beda6-183">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="beda6-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span><span class="sxs-lookup"><span data-stu-id="beda6-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="beda6-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span><span class="sxs-lookup"><span data-stu-id="beda6-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="beda6-186">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span><span class="sxs-lookup"><span data-stu-id="beda6-186">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="beda6-187">Start with retrieving the subscription tenant ID.</span><span class="sxs-lookup"><span data-stu-id="beda6-187">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="beda6-188">You will need that later.</span><span class="sxs-lookup"><span data-stu-id="beda6-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="beda6-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="beda6-190">The default storage will still be the Azure storage blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="beda6-190">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="beda6-191">So, we'll first create the storage account and storage containers required for the cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-191">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="beda6-192">Create the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="beda6-192">Create the HDInsight cluster.</span></span> <span data-ttu-id="beda6-193">Use the following cmdlets.</span><span class="sxs-lookup"><span data-stu-id="beda6-193">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="beda6-194">After the cmdlet successfully completes, you should see an output listing the cluster details.</span><span class="sxs-lookup"><span data-stu-id="beda6-194">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="beda6-195">Run test jobs on the HDInsight cluster to use the Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-195">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="beda6-196">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-196">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="beda6-197">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-197">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="beda6-198">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span><span class="sxs-lookup"><span data-stu-id="beda6-198">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="beda6-199">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="beda6-199">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="beda6-200">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="beda6-200">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="beda6-201">Once connected, start the Hive CLI by using the following command:</span><span class="sxs-lookup"><span data-stu-id="beda6-201">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="beda6-202">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="beda6-202">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="beda6-203">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="beda6-203">You should see an output similar to the following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="beda6-204">Access Data Lake Store using HDFS commands</span><span class="sxs-lookup"><span data-stu-id="beda6-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="beda6-205">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span><span class="sxs-lookup"><span data-stu-id="beda6-205">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="beda6-206">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span><span class="sxs-lookup"><span data-stu-id="beda6-206">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="beda6-207">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="beda6-207">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="beda6-208">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="beda6-208">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="beda6-209">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-209">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="beda6-210">This should list the file that you uploaded earlier to the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="beda6-210">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="beda6-211">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span><span class="sxs-lookup"><span data-stu-id="beda6-211">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="beda6-212">See Also</span><span class="sxs-lookup"><span data-stu-id="beda6-212">See Also</span></span>
* [<span data-ttu-id="beda6-213">Portal: Create an HDInsight cluster to use Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="beda6-213">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx


