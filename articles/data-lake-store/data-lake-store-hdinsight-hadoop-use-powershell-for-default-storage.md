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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/02/2017
ms.author: nitinme
ms.openlocfilehash: aa3efb449f02a40e726c377f5761df41a07e2c51
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552887"
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Create HDInsight clusters with Data Lake Store as default storage by using PowerShell
> [!div class="op_single_selector"]
> * [Use the Azure portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Use PowerShell (for default storage)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Use PowerShell (for additional storage)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Use Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage. For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).

Here are some important considerations for using HDInsight with Data Lake Store:

* The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5.

* The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.

* For HBase clusters (Windows and Linux), Data Lake Store is *not supported* as a storage option for either default and additional storage.

To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.

## <a name="prerequisites"></a>Prerequisites
Before you begin this tutorial, make sure that you meet the following requirements:

* **An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azureps-cmdlets-docs).
* **Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads). You use Windows SDK to create a security certificate.
* **Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD). However, to create a service principal, you must be an Azure AD administrator. If you are an administrator, you can skip this prerequisite and proceed with the tutorial.

    >[!NOTE]
    >You can create a service principal only if you are an Azure AD administrator. Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store. The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Create a Data Lake Store account
To create a Data Lake Store account, do the following:

1. From your desktop, open a PowerShell window, and then enter the following snippet:

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store. To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).
    >

2. When you are prompted to sign in, sign in as one of the subscription administrators or owners.
3. A Data Lake Store account is associated with an Azure resource group. Start by creating a resource group.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Create an Azure resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure resource group")
3. Create a Data Lake Store account. The account name you specify must contain only lowercase letters and numbers.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Create an Azure Data Lake account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-hdinsight-hadoop-use-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake account")
4. Verify that the account has been created successfully.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    The output should be **True**.

5. Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation. To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a>Set up authentication for role-based access to Data Lake Store
Every Azure subscription is associated with an Azure AD entity. Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD. Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource. For services, a service principal identifies the service in Azure AD.

This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier). You do so by creating a service principal for the application and assigning roles to it via PowerShell.

To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.

### <a name="create-a-self-signed-certificate"></a>Create a self-signed certificate
Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section. You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.

1. From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key. Use the following commands:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    You will be prompted to enter the private key password. After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.
2. Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file. Run the following command:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    When you are prompted, enter the private key password that you specified earlier. The value you specify for the **-po** parameter is the password that's associated with the .pfx file. After the command has been completed successfully, you should also see a CertFile.pfx in the certificate directory that you specified.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Create an Azure AD and a service principal
In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate. To create an application in Azure AD, run the following commands:

1. Paste the following cmdlets in the PowerShell console window. Make sure that the value you specify for the **-DisplayName** property is unique. The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.

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
2. Create a service principal by using the application ID.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier. Use the following cmdlets:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a>Create an HDInsight Linux cluster with Data Lake Store as the default storage

In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage. For this release, the HDInsight cluster and Data Lake Store must be in the same location.

1. Retrieve the subscription tenant ID, and store it to use later.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Create the HDInsight cluster by using the following cmdlets:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
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
               -Version "3.5" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    After the cmdlet has been successfully completed, you should see an output that lists the cluster details.

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a>Run test jobs on the HDInsight cluster to use Data Lake Store
After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store. To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.

In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.

* If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. After you have made the connection, start the Hive command-line interface (CLI) by using the following command:

        hive
2. Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    You should see the query output on the SSH console.

    >[!NOTE]
    >The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root. Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. You can either use the shorter alternative or provide the complete path to the cluster root.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Access Data Lake Store by using HDFS commands
After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.

In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.

* If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.

    hdfs dfs -ls adl:///

You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.

## <a name="see-also"></a>See also
* [Azure portal: Create an HDInsight cluster to use Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx

