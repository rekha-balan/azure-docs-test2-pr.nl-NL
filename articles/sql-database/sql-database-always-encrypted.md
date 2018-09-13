---
title: 'Always Encrypted: Azure SQL Database - Windows certificate store | Microsoft Docs'
description: This article shows you how to secure sensitive data in a SQL database with database encryption by using the Always Encrypted Wizard in SQL Server Management Studio (SSMS). It also shows you how to store your encryption keys in the Windows certificate store.
keywords: encrypt data, sql encryption, database encryption, sensitive data, Always Encrypted
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security-protect
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 683b8efddc2fd30c10a67ecf0e65a35e7434346b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564301"
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="2efbc-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span><span class="sxs-lookup"><span data-stu-id="2efbc-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="2efbc-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="2efbc-107">It also shows you how to store your encryption keys in the Windows certificate store.</span><span class="sxs-lookup"><span data-stu-id="2efbc-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="2efbc-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span><span class="sxs-lookup"><span data-stu-id="2efbc-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="2efbc-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span><span class="sxs-lookup"><span data-stu-id="2efbc-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="2efbc-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="2efbc-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span><span class="sxs-lookup"><span data-stu-id="2efbc-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="2efbc-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="2efbc-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="2efbc-113">In this article, you will learn how to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="2efbc-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="2efbc-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="2efbc-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="2efbc-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="2efbc-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="2efbc-117">Create a database table and encrypt columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="2efbc-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2efbc-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2efbc-119">Prerequisites</span></span>
<span data-ttu-id="2efbc-120">For this tutorial, you'll need:</span><span class="sxs-lookup"><span data-stu-id="2efbc-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="2efbc-121">An Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="2efbc-121">An Azure account and subscription.</span></span> <span data-ttu-id="2efbc-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2efbc-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2efbc-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span><span class="sxs-lookup"><span data-stu-id="2efbc-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="2efbc-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span><span class="sxs-lookup"><span data-stu-id="2efbc-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="2efbc-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="2efbc-126">Create a blank SQL database</span><span class="sxs-lookup"><span data-stu-id="2efbc-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="2efbc-127">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2efbc-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2efbc-128">Click **New** > **Data + Storage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="2efbc-129">Create a **Blank** database named **Clinic** on a new or existing server.</span><span class="sxs-lookup"><span data-stu-id="2efbc-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="2efbc-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2efbc-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Create a blank database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="2efbc-132">You will need the connection string later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2efbc-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="2efbc-133">After the database is created, go to the new Clinic database and copy the connection string.</span><span class="sxs-lookup"><span data-stu-id="2efbc-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="2efbc-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2efbc-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="2efbc-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="2efbc-136">Copy the connection string for **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copy the connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="2efbc-138">Connect to the database with SSMS</span><span class="sxs-lookup"><span data-stu-id="2efbc-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="2efbc-139">Open SSMS and connect to the server with the Clinic database.</span><span class="sxs-lookup"><span data-stu-id="2efbc-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="2efbc-140">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="2efbc-140">Open SSMS.</span></span> <span data-ttu-id="2efbc-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span><span class="sxs-lookup"><span data-stu-id="2efbc-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="2efbc-142">Enter your server name and credentials.</span><span class="sxs-lookup"><span data-stu-id="2efbc-142">Enter your server name and credentials.</span></span> <span data-ttu-id="2efbc-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="2efbc-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="2efbc-144">Type the complete server name including *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="2efbc-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![Copy the connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="2efbc-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span><span class="sxs-lookup"><span data-stu-id="2efbc-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="2efbc-147">Create a table</span><span class="sxs-lookup"><span data-stu-id="2efbc-147">Create a table</span></span>
<span data-ttu-id="2efbc-148">In this section, you will create a table to hold patient data.</span><span class="sxs-lookup"><span data-stu-id="2efbc-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="2efbc-149">This will be a normal table initially--you will configure encryption in the next section.</span><span class="sxs-lookup"><span data-stu-id="2efbc-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="2efbc-150">Expand **Databases**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="2efbc-151">Right-click the **Clinic** database and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="2efbc-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span><span class="sxs-lookup"><span data-stu-id="2efbc-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="2efbc-153">Encrypt columns (configure Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="2efbc-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="2efbc-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span><span class="sxs-lookup"><span data-stu-id="2efbc-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="2efbc-155">Expand **Databases** > **Clinic** > **Tables**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="2efbc-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span><span class="sxs-lookup"><span data-stu-id="2efbc-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Encrypt columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="2efbc-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="2efbc-159">Column Selection</span><span class="sxs-lookup"><span data-stu-id="2efbc-159">Column Selection</span></span>
<span data-ttu-id="2efbc-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span><span class="sxs-lookup"><span data-stu-id="2efbc-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="2efbc-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span><span class="sxs-lookup"><span data-stu-id="2efbc-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="2efbc-162">Encrypt **SSN** and **BirthDate** information for each patient.</span><span class="sxs-lookup"><span data-stu-id="2efbc-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="2efbc-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span><span class="sxs-lookup"><span data-stu-id="2efbc-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="2efbc-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span><span class="sxs-lookup"><span data-stu-id="2efbc-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="2efbc-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="2efbc-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-166">Click **Next**.</span></span>

![Encrypt columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="2efbc-168">Master Key Configuration</span><span class="sxs-lookup"><span data-stu-id="2efbc-168">Master Key Configuration</span></span>
<span data-ttu-id="2efbc-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span><span class="sxs-lookup"><span data-stu-id="2efbc-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="2efbc-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span><span class="sxs-lookup"><span data-stu-id="2efbc-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="2efbc-171">This tutorial shows how to store your keys in the Windows certificate store.</span><span class="sxs-lookup"><span data-stu-id="2efbc-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="2efbc-172">Verify that **Windows certificate store** is selected and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Master key configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="2efbc-174">Validation</span><span class="sxs-lookup"><span data-stu-id="2efbc-174">Validation</span></span>
<span data-ttu-id="2efbc-175">You can encrypt the columns now or save a PowerShell script to run later.</span><span class="sxs-lookup"><span data-stu-id="2efbc-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="2efbc-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="2efbc-177">Summary</span><span class="sxs-lookup"><span data-stu-id="2efbc-177">Summary</span></span>
<span data-ttu-id="2efbc-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="2efbc-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="2efbc-180">Verify the wizard's actions</span><span class="sxs-lookup"><span data-stu-id="2efbc-180">Verify the wizard's actions</span></span>
<span data-ttu-id="2efbc-181">After the wizard is finished, your database is set up for Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="2efbc-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="2efbc-182">The wizard performed the following actions:</span><span class="sxs-lookup"><span data-stu-id="2efbc-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="2efbc-183">Created a CMK.</span><span class="sxs-lookup"><span data-stu-id="2efbc-183">Created a CMK.</span></span>
* <span data-ttu-id="2efbc-184">Created a CEK.</span><span class="sxs-lookup"><span data-stu-id="2efbc-184">Created a CEK.</span></span>
* <span data-ttu-id="2efbc-185">Configured the selected columns for encryption.</span><span class="sxs-lookup"><span data-stu-id="2efbc-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="2efbc-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span><span class="sxs-lookup"><span data-stu-id="2efbc-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="2efbc-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="2efbc-188">You can now see the new keys that the wizard generated for you.</span><span class="sxs-lookup"><span data-stu-id="2efbc-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="2efbc-189">Create a client application that works with the encrypted data</span><span class="sxs-lookup"><span data-stu-id="2efbc-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="2efbc-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="2efbc-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span><span class="sxs-lookup"><span data-stu-id="2efbc-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="2efbc-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span><span class="sxs-lookup"><span data-stu-id="2efbc-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2efbc-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="2efbc-194">Passing literal values without using SqlParameter objects will result in an exception.</span><span class="sxs-lookup"><span data-stu-id="2efbc-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="2efbc-195">Open Visual Studio and create a new C# console application.</span><span class="sxs-lookup"><span data-stu-id="2efbc-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="2efbc-196">Make sure your project is set to **.NET Framework 4.6** or later.</span><span class="sxs-lookup"><span data-stu-id="2efbc-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="2efbc-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="2efbc-199">Modify your connection string to enable Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="2efbc-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="2efbc-200">This section explains how to enable Always Encrypted in your database connection string.</span><span class="sxs-lookup"><span data-stu-id="2efbc-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="2efbc-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span><span class="sxs-lookup"><span data-stu-id="2efbc-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="2efbc-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="2efbc-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="2efbc-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="2efbc-205">This is the only change required in a client application specific to Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="2efbc-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="2efbc-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span><span class="sxs-lookup"><span data-stu-id="2efbc-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="2efbc-207">Enable Always Encrypted in the connection string</span><span class="sxs-lookup"><span data-stu-id="2efbc-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="2efbc-208">Add the following keyword to your connection string:</span><span class="sxs-lookup"><span data-stu-id="2efbc-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="2efbc-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="2efbc-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="2efbc-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="2efbc-211">Always Encrypted sample console application</span><span class="sxs-lookup"><span data-stu-id="2efbc-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="2efbc-212">This sample demonstrates how to:</span><span class="sxs-lookup"><span data-stu-id="2efbc-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="2efbc-213">Modify your connection string to enable Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="2efbc-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="2efbc-214">Insert data into the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="2efbc-215">Select a record by filtering for a specific value in an encrypted column.</span><span class="sxs-lookup"><span data-stu-id="2efbc-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="2efbc-216">Replace the contents of **Program.cs** with the following code.</span><span class="sxs-lookup"><span data-stu-id="2efbc-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="2efbc-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2efbc-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="2efbc-218">This is the only change you need to make to this code.</span><span class="sxs-lookup"><span data-stu-id="2efbc-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="2efbc-219">Run the app to see Always Encrypted in action.</span><span class="sxs-lookup"><span data-stu-id="2efbc-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="2efbc-220">Verify that the data is encrypted</span><span class="sxs-lookup"><span data-stu-id="2efbc-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="2efbc-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span><span class="sxs-lookup"><span data-stu-id="2efbc-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="2efbc-222">(Use your current connection where the column encryption setting is not yet enabled.)</span><span class="sxs-lookup"><span data-stu-id="2efbc-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="2efbc-223">Run the following query on the Clinic database.</span><span class="sxs-lookup"><span data-stu-id="2efbc-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="2efbc-224">You can see that the encrypted columns do not contain any plaintext data.</span><span class="sxs-lookup"><span data-stu-id="2efbc-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="2efbc-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span><span class="sxs-lookup"><span data-stu-id="2efbc-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="2efbc-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="2efbc-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="2efbc-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="2efbc-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="2efbc-231">Run the following query on the **Clinic** database.</span><span class="sxs-lookup"><span data-stu-id="2efbc-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="2efbc-232">You can now see the plaintext data in the encrypted columns.</span><span class="sxs-lookup"><span data-stu-id="2efbc-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![New console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="2efbc-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span><span class="sxs-lookup"><span data-stu-id="2efbc-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2efbc-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="2efbc-235">Next steps</span></span>
<span data-ttu-id="2efbc-236">After you create a database that uses Always Encrypted, you may want to do the following:</span><span class="sxs-lookup"><span data-stu-id="2efbc-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="2efbc-237">Run this sample from a different computer.</span><span class="sxs-lookup"><span data-stu-id="2efbc-237">Run this sample from a different computer.</span></span> <span data-ttu-id="2efbc-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span><span class="sxs-lookup"><span data-stu-id="2efbc-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="2efbc-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="2efbc-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="2efbc-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="2efbc-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span><span class="sxs-lookup"><span data-stu-id="2efbc-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="2efbc-242">Related information</span><span class="sxs-lookup"><span data-stu-id="2efbc-242">Related information</span></span>
* [<span data-ttu-id="2efbc-243">Always Encrypted (client development)</span><span class="sxs-lookup"><span data-stu-id="2efbc-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="2efbc-244">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="2efbc-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="2efbc-245">SQL Server Encryption</span><span class="sxs-lookup"><span data-stu-id="2efbc-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="2efbc-246">Always Encrypted Wizard</span><span class="sxs-lookup"><span data-stu-id="2efbc-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="2efbc-247">Always Encrypted Blog</span><span class="sxs-lookup"><span data-stu-id="2efbc-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)












