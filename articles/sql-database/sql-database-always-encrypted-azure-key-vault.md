---
title: 'Always Encrypted: SQL Database - Azure Key Vault | Microsoft Docs'
description: This article shows you how to secure sensitive data in a SQL database with data encryption using the Always Encrypted Wizard in SQL Server Management Studio. It also includes instructions that will show you how to store each encryption key in Azure Key Vault.
keywords: data encryption, encryption key, cloud encryption
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security-protect
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 2f9d227be93433eae87ab776f3dc4a5e618a2b26
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555333"
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="c06d4-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c06d4-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="c06d4-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="c06d4-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c06d4-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="c06d4-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span><span class="sxs-lookup"><span data-stu-id="c06d4-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span></span> <span data-ttu-id="c06d4-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span><span class="sxs-lookup"><span data-stu-id="c06d4-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="c06d4-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span><span class="sxs-lookup"><span data-stu-id="c06d4-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="c06d4-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="c06d4-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span><span class="sxs-lookup"><span data-stu-id="c06d4-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="c06d4-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c06d4-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="c06d4-114">In this article you will learn how to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c06d4-114">In this article you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="c06d4-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="c06d4-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="c06d4-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="c06d4-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="c06d4-118">Create a database table and encrypt columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="c06d4-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c06d4-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c06d4-120">Prerequisites</span></span>
<span data-ttu-id="c06d4-121">For this tutorial, you'll need:</span><span class="sxs-lookup"><span data-stu-id="c06d4-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="c06d4-122">An Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="c06d4-122">An Azure account and subscription.</span></span> <span data-ttu-id="c06d4-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c06d4-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c06d4-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span><span class="sxs-lookup"><span data-stu-id="c06d4-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="c06d4-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span><span class="sxs-lookup"><span data-stu-id="c06d4-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="c06d4-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="c06d4-127">[Azure PowerShell](/powershell/azureps-cmdlets-docs), version  1.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c06d4-127">[Azure PowerShell](/powershell/azureps-cmdlets-docs), version  1.0 or later.</span></span> <span data-ttu-id="c06d4-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span><span class="sxs-lookup"><span data-stu-id="c06d4-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-to-access-the-sql-database-service"></a><span data-ttu-id="c06d4-129">Enable your client application to access the SQL Database service</span><span class="sxs-lookup"><span data-stu-id="c06d4-129">Enable your client application to access the SQL Database service</span></span>
<span data-ttu-id="c06d4-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span><span class="sxs-lookup"><span data-stu-id="c06d4-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span></span>

1. <span data-ttu-id="c06d4-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c06d4-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c06d4-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span><span class="sxs-lookup"><span data-stu-id="c06d4-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="c06d4-133">Click **Applications**, and then click **ADD**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="c06d4-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span><span class="sxs-lookup"><span data-stu-id="c06d4-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span></span>
5. <span data-ttu-id="c06d4-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span><span class="sxs-lookup"><span data-stu-id="c06d4-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="c06d4-136">Click **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="c06d4-137">Copy your **CLIENT ID**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="c06d4-138">(You will need this value in your code later.)</span><span class="sxs-lookup"><span data-stu-id="c06d4-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="c06d4-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c06d4-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span></span> <span data-ttu-id="c06d4-140">(You will copy the key after you save in step 13.)</span><span class="sxs-lookup"><span data-stu-id="c06d4-140">(You will copy the key after you save in step 13.)</span></span>
9. <span data-ttu-id="c06d4-141">Scroll down and click **Add application**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="c06d4-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="c06d4-143">Click the checkmark to continue.</span><span class="sxs-lookup"><span data-stu-id="c06d4-143">Click the checkmark to continue.</span></span>
11. <span data-ttu-id="c06d4-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c06d4-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="c06d4-145">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="c06d4-146">After the save finishes, copy the key value in the **keys** section.</span><span class="sxs-lookup"><span data-stu-id="c06d4-146">After the save finishes, copy the key value in the **keys** section.</span></span> <span data-ttu-id="c06d4-147">(You will need this value in your code later.)</span><span class="sxs-lookup"><span data-stu-id="c06d4-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-to-store-your-keys"></a><span data-ttu-id="c06d4-148">Create a key vault to store your keys</span><span class="sxs-lookup"><span data-stu-id="c06d4-148">Create a key vault to store your keys</span></span>
<span data-ttu-id="c06d4-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span><span class="sxs-lookup"><span data-stu-id="c06d4-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span></span> <span data-ttu-id="c06d4-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c06d4-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="c06d4-151">You can quickly create a key vault by running the following script.</span><span class="sxs-lookup"><span data-stu-id="c06d4-151">You can quickly create a key vault by running the following script.</span></span> <span data-ttu-id="c06d4-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c06d4-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).SubscriptionId
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="c06d4-153">Create a blank SQL database</span><span class="sxs-lookup"><span data-stu-id="c06d4-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="c06d4-154">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c06d4-154">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c06d4-155">Go to **New** > **Data + Storage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-155">Go to **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="c06d4-156">Create a **Blank** database named **Clinic** on a new or existing server.</span><span class="sxs-lookup"><span data-stu-id="c06d4-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="c06d4-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c06d4-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Create a blank database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="c06d4-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span><span class="sxs-lookup"><span data-stu-id="c06d4-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span></span> <span data-ttu-id="c06d4-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c06d4-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span></span>

1. <span data-ttu-id="c06d4-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="c06d4-162">Copy the connection string for **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-162">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copy the connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="c06d4-164">Connect to the database with SSMS</span><span class="sxs-lookup"><span data-stu-id="c06d4-164">Connect to the database with SSMS</span></span>
<span data-ttu-id="c06d4-165">Open SSMS and connect to the server with the Clinic database.</span><span class="sxs-lookup"><span data-stu-id="c06d4-165">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="c06d4-166">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="c06d4-166">Open SSMS.</span></span> <span data-ttu-id="c06d4-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span><span class="sxs-lookup"><span data-stu-id="c06d4-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span></span>
2. <span data-ttu-id="c06d4-168">Enter your server name and credentials.</span><span class="sxs-lookup"><span data-stu-id="c06d4-168">Enter your server name and credentials.</span></span> <span data-ttu-id="c06d4-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="c06d4-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="c06d4-170">Type the complete server name, including *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c06d4-170">Type the complete server name, including *database.windows.net*.</span></span>
   
    ![Copy the connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="c06d4-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span><span class="sxs-lookup"><span data-stu-id="c06d4-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c06d4-173">Create a table</span><span class="sxs-lookup"><span data-stu-id="c06d4-173">Create a table</span></span>
<span data-ttu-id="c06d4-174">In this section, you will create a table to hold patient data.</span><span class="sxs-lookup"><span data-stu-id="c06d4-174">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="c06d4-175">It's not initially encrypted--you will configure encryption in the next section.</span><span class="sxs-lookup"><span data-stu-id="c06d4-175">It's not initially encrypted--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="c06d4-176">Expand **Databases**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="c06d4-177">Right-click the **Clinic** database and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-177">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="c06d4-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span><span class="sxs-lookup"><span data-stu-id="c06d4-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="c06d4-179">Encrypt columns (configure Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="c06d4-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="c06d4-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span><span class="sxs-lookup"><span data-stu-id="c06d4-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="c06d4-181">Expand **Databases** > **Clinic** > **Tables**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="c06d4-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span><span class="sxs-lookup"><span data-stu-id="c06d4-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Encrypt columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="c06d4-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="c06d4-185">Column Selection</span><span class="sxs-lookup"><span data-stu-id="c06d4-185">Column Selection</span></span>
<span data-ttu-id="c06d4-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span><span class="sxs-lookup"><span data-stu-id="c06d4-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="c06d4-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span><span class="sxs-lookup"><span data-stu-id="c06d4-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="c06d4-188">Encrypt **SSN** and **BirthDate** information for each patient.</span><span class="sxs-lookup"><span data-stu-id="c06d4-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="c06d4-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span><span class="sxs-lookup"><span data-stu-id="c06d4-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="c06d4-190">The BirthDate column will use randomized encryption, which does not support operations.</span><span class="sxs-lookup"><span data-stu-id="c06d4-190">The BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="c06d4-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span></span> <span data-ttu-id="c06d4-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-192">Click **Next**.</span></span>

![Encrypt columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="c06d4-194">Master Key Configuration</span><span class="sxs-lookup"><span data-stu-id="c06d4-194">Master Key Configuration</span></span>
<span data-ttu-id="c06d4-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span><span class="sxs-lookup"><span data-stu-id="c06d4-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="c06d4-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span><span class="sxs-lookup"><span data-stu-id="c06d4-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="c06d4-197">This tutorial shows how to store your keys in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c06d4-197">This tutorial shows how to store your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="c06d4-198">Select **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="c06d4-199">Select the desired key vault from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="c06d4-199">Select the desired key vault from the drop-down list.</span></span>
3. <span data-ttu-id="c06d4-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-200">Click **Next**.</span></span>

![Master key configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="c06d4-202">Validation</span><span class="sxs-lookup"><span data-stu-id="c06d4-202">Validation</span></span>
<span data-ttu-id="c06d4-203">You can encrypt the columns now or save a PowerShell script to run later.</span><span class="sxs-lookup"><span data-stu-id="c06d4-203">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="c06d4-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="c06d4-205">Summary</span><span class="sxs-lookup"><span data-stu-id="c06d4-205">Summary</span></span>
<span data-ttu-id="c06d4-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="c06d4-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="c06d4-208">Verify the wizard's actions</span><span class="sxs-lookup"><span data-stu-id="c06d4-208">Verify the wizard's actions</span></span>
<span data-ttu-id="c06d4-209">After the wizard is finished, your database is set up for Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="c06d4-209">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="c06d4-210">The wizard performed the following actions:</span><span class="sxs-lookup"><span data-stu-id="c06d4-210">The wizard performed the following actions:</span></span>

* <span data-ttu-id="c06d4-211">Created a column master key and stored it in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c06d4-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="c06d4-212">Created a column encryption key and stored it in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c06d4-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="c06d4-213">Configured the selected columns for encryption.</span><span class="sxs-lookup"><span data-stu-id="c06d4-213">Configured the selected columns for encryption.</span></span> <span data-ttu-id="c06d4-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span><span class="sxs-lookup"><span data-stu-id="c06d4-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="c06d4-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="c06d4-216">Create a client application that works with the encrypted data</span><span class="sxs-lookup"><span data-stu-id="c06d4-216">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="c06d4-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c06d4-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="c06d4-219">Passing literal values without using SqlParameter objects will result in an exception.</span><span class="sxs-lookup"><span data-stu-id="c06d4-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="c06d4-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span><span class="sxs-lookup"><span data-stu-id="c06d4-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="c06d4-221">Make sure your project is set to **.NET Framework 4.6** or later.</span><span class="sxs-lookup"><span data-stu-id="c06d4-221">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="c06d4-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="c06d4-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="c06d4-224">Run these two lines of code in the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="c06d4-224">Run these two lines of code in the Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="c06d4-225">Modify your connection string to enable Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="c06d4-225">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="c06d4-226">This section  explains how to enable Always Encrypted in your database connection string.</span><span class="sxs-lookup"><span data-stu-id="c06d4-226">This section  explains how to enable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="c06d4-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="c06d4-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="c06d4-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="c06d4-230">Enable Always Encrypted in the connection string</span><span class="sxs-lookup"><span data-stu-id="c06d4-230">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="c06d4-231">Add the following keyword to your connection string.</span><span class="sxs-lookup"><span data-stu-id="c06d4-231">Add the following keyword to your connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="c06d4-232">Enable Always Encrypted with SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="c06d4-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="c06d4-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-the-azure-key-vault-provider"></a><span data-ttu-id="c06d4-234">Register the Azure Key Vault provider</span><span class="sxs-lookup"><span data-stu-id="c06d4-234">Register the Azure Key Vault provider</span></span>
<span data-ttu-id="c06d4-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span><span class="sxs-lookup"><span data-stu-id="c06d4-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="c06d4-236">Always Encrypted sample console application</span><span class="sxs-lookup"><span data-stu-id="c06d4-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="c06d4-237">This sample demonstrates how to:</span><span class="sxs-lookup"><span data-stu-id="c06d4-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="c06d4-238">Modify your connection string to enable Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="c06d4-238">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="c06d4-239">Register Azure Key Vault as the application's key store provider.</span><span class="sxs-lookup"><span data-stu-id="c06d4-239">Register Azure Key Vault as the application's key store provider.</span></span>  
* <span data-ttu-id="c06d4-240">Insert data into the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-240">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="c06d4-241">Select a record by filtering for a specific value in an encrypted column.</span><span class="sxs-lookup"><span data-stu-id="c06d4-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="c06d4-242">Replace the contents of **Program.cs** with the following code.</span><span class="sxs-lookup"><span data-stu-id="c06d4-242">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="c06d4-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c06d4-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="c06d4-244">This is the only change you need to make to this code.</span><span class="sxs-lookup"><span data-stu-id="c06d4-244">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="c06d4-245">Run the app to see Always Encrypted in action.</span><span class="sxs-lookup"><span data-stu-id="c06d4-245">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"<connection string from the portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed to obtain the access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in the Patients table to reset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="c06d4-246">Verify that the data is encrypted</span><span class="sxs-lookup"><span data-stu-id="c06d4-246">Verify that the data is encrypted</span></span>
<span data-ttu-id="c06d4-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span><span class="sxs-lookup"><span data-stu-id="c06d4-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="c06d4-248">Run the following query on the Clinic database.</span><span class="sxs-lookup"><span data-stu-id="c06d4-248">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="c06d4-249">You can see that the encrypted columns do not contain any plaintext data.</span><span class="sxs-lookup"><span data-stu-id="c06d4-249">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="c06d4-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span><span class="sxs-lookup"><span data-stu-id="c06d4-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span></span>

1. <span data-ttu-id="c06d4-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="c06d4-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span></span>
3. <span data-ttu-id="c06d4-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="c06d4-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="c06d4-256">Run the following query on the Clinic database.</span><span class="sxs-lookup"><span data-stu-id="c06d4-256">Run the following query on the Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="c06d4-257">You can now see the plaintext data in the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="c06d4-257">You can now see the plaintext data in the encrypted columns.</span></span>

    ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="c06d4-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="c06d4-259">Next steps</span></span>
<span data-ttu-id="c06d4-260">After you create a database that uses Always Encrypted, you may want to do the following:</span><span class="sxs-lookup"><span data-stu-id="c06d4-260">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="c06d4-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="c06d4-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="c06d4-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="c06d4-263">Related information</span><span class="sxs-lookup"><span data-stu-id="c06d4-263">Related information</span></span>
* [<span data-ttu-id="c06d4-264">Always Encrypted (client development)</span><span class="sxs-lookup"><span data-stu-id="c06d4-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="c06d4-265">Transparent data encryption</span><span class="sxs-lookup"><span data-stu-id="c06d4-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="c06d4-266">SQL Server encryption</span><span class="sxs-lookup"><span data-stu-id="c06d4-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="c06d4-267">Always Encrypted wizard</span><span class="sxs-lookup"><span data-stu-id="c06d4-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="c06d4-268">Always Encrypted blog</span><span class="sxs-lookup"><span data-stu-id="c06d4-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)











