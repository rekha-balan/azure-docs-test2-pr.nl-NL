---
title: Create HDInsight clusters with Data Lake Store as default storage by using PowerShell | Microsoft Docs'
description: Use Azure PowerShell to create and use HDInsight clusters with Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: da48602bddc61b0df93cfdda613219381aed1e8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44777055"
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="7d52e-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d52e-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Use the Azure portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Use PowerShell (for default storage)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Use PowerShell (for additional storage)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Use Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="7d52e-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span><span class="sxs-lookup"><span data-stu-id="7d52e-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="7d52e-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7d52e-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="7d52e-110">Here are some important considerations for using HDInsight with Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="7d52e-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="7d52e-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="7d52e-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="7d52e-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span><span class="sxs-lookup"><span data-stu-id="7d52e-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="7d52e-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span><span class="sxs-lookup"><span data-stu-id="7d52e-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d52e-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d52e-114">Prerequisites</span></span>

<span data-ttu-id="7d52e-115">Before you begin this tutorial, make sure that you meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="7d52e-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="7d52e-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d52e-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7d52e-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d52e-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="7d52e-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="7d52e-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/downloads).</span></span> <span data-ttu-id="7d52e-119">The SDK is used to create a security certificate.</span><span class="sxs-lookup"><span data-stu-id="7d52e-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="7d52e-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d52e-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7d52e-121">However, to create a service principal, you must be an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="7d52e-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="7d52e-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span><span class="sxs-lookup"><span data-stu-id="7d52e-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    >You can create a service principal only if you are an Azure AD administrator. Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store. The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="7d52e-126">Create a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="7d52e-126">Create a Data Lake Store account</span></span>

<span data-ttu-id="7d52e-127">To create a Data Lake Store account, do the following:</span><span class="sxs-lookup"><span data-stu-id="7d52e-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="7d52e-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span><span class="sxs-lookup"><span data-stu-id="7d52e-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="7d52e-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span><span class="sxs-lookup"><span data-stu-id="7d52e-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Connect-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store. To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).
    >

2. <span data-ttu-id="7d52e-132">A Data Lake Store account is associated with an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="7d52e-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="7d52e-133">Start by creating a resource group.</span><span class="sxs-lookup"><span data-stu-id="7d52e-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="7d52e-134">You should see an output like this:</span><span class="sxs-lookup"><span data-stu-id="7d52e-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="7d52e-135">Create a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="7d52e-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="7d52e-136">The account name you specify must contain only lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="7d52e-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="7d52e-137">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="7d52e-137">You should see an output like the following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. <span data-ttu-id="7d52e-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="7d52e-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="7d52e-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="7d52e-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="7d52e-140">Set up authentication for role-based access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7d52e-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="7d52e-141">Every Azure subscription is associated with an Azure AD entity.</span><span class="sxs-lookup"><span data-stu-id="7d52e-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="7d52e-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d52e-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="7d52e-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span><span class="sxs-lookup"><span data-stu-id="7d52e-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="7d52e-144">For services, a service principal identifies the service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d52e-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="7d52e-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span><span class="sxs-lookup"><span data-stu-id="7d52e-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="7d52e-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d52e-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="7d52e-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span><span class="sxs-lookup"><span data-stu-id="7d52e-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="7d52e-148">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="7d52e-148">Create a self-signed certificate</span></span>
<span data-ttu-id="7d52e-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="7d52e-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="7d52e-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span><span class="sxs-lookup"><span data-stu-id="7d52e-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="7d52e-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span><span class="sxs-lookup"><span data-stu-id="7d52e-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="7d52e-152">Use the following commands:</span><span class="sxs-lookup"><span data-stu-id="7d52e-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="7d52e-153">You will be prompted to enter the private key password.</span><span class="sxs-lookup"><span data-stu-id="7d52e-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="7d52e-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span><span class="sxs-lookup"><span data-stu-id="7d52e-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="7d52e-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span><span class="sxs-lookup"><span data-stu-id="7d52e-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="7d52e-156">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="7d52e-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="7d52e-157">When you are prompted, enter the private key password that you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="7d52e-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="7d52e-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="7d52e-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="7d52e-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span><span class="sxs-lookup"><span data-stu-id="7d52e-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="7d52e-160">Create an Azure AD and a service principal</span><span class="sxs-lookup"><span data-stu-id="7d52e-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="7d52e-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span><span class="sxs-lookup"><span data-stu-id="7d52e-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="7d52e-162">To create an application in Azure AD, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7d52e-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="7d52e-163">Paste the following cmdlets in the PowerShell console window.</span><span class="sxs-lookup"><span data-stu-id="7d52e-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="7d52e-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span><span class="sxs-lookup"><span data-stu-id="7d52e-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="7d52e-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span><span class="sxs-lookup"><span data-stu-id="7d52e-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host -Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="7d52e-166">Create a service principal by using the application ID.</span><span class="sxs-lookup"><span data-stu-id="7d52e-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="7d52e-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="7d52e-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="7d52e-168">Use the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="7d52e-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="7d52e-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span><span class="sxs-lookup"><span data-stu-id="7d52e-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="7d52e-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span><span class="sxs-lookup"><span data-stu-id="7d52e-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="7d52e-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span><span class="sxs-lookup"><span data-stu-id="7d52e-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="7d52e-172">Retrieve the subscription tenant ID, and store it to use later.</span><span class="sxs-lookup"><span data-stu-id="7d52e-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="7d52e-173">Create the HDInsight cluster by using the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="7d52e-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="7d52e-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span><span class="sxs-lookup"><span data-stu-id="7d52e-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="7d52e-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7d52e-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="7d52e-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7d52e-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="7d52e-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="7d52e-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="7d52e-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span><span class="sxs-lookup"><span data-stu-id="7d52e-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="7d52e-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7d52e-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="7d52e-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7d52e-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="7d52e-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span><span class="sxs-lookup"><span data-stu-id="7d52e-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="7d52e-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="7d52e-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="7d52e-183">You should see the query output on the SSH console.</span><span class="sxs-lookup"><span data-stu-id="7d52e-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    >The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root. Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. You can either use the shorter alternative or provide the complete path to the cluster root.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="7d52e-187">Access Data Lake Store by using HDFS commands</span><span class="sxs-lookup"><span data-stu-id="7d52e-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="7d52e-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span><span class="sxs-lookup"><span data-stu-id="7d52e-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="7d52e-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span><span class="sxs-lookup"><span data-stu-id="7d52e-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="7d52e-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7d52e-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="7d52e-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7d52e-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7d52e-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span><span class="sxs-lookup"><span data-stu-id="7d52e-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="7d52e-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span><span class="sxs-lookup"><span data-stu-id="7d52e-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="7d52e-194">See also</span><span class="sxs-lookup"><span data-stu-id="7d52e-194">See also</span></span>
* [<span data-ttu-id="7d52e-195">Use Data Lake Store with Azure HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="7d52e-195">Use Data Lake Store with Azure HDInsight clusters</span></span>](../hdinsight/hdinsight-hadoop-use-data-lake-store.md)
* [<span data-ttu-id="7d52e-196">Azure portal: Create an HDInsight cluster to use Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7d52e-196">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
