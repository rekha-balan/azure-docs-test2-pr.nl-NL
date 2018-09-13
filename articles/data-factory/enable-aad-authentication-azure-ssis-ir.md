---
title: Enable Azure Active Directory Authentication for the Azure-SSIS integration runtime | Microsoft Docs
description: This article describes how to configure the Azure-SSIS integration runtime to enable connections that use Azure Active Directory authentication.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: conceptual
ms.date: 06/21/2018
ms.author: douglasl
ms.openlocfilehash: 93d3e25957fb1f04400fa78423a5658d32f7d5fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868588"
---
# <a name="enable-azure-active-directory-authentication-for-the-azure-ssis-integration-runtime"></a><span data-ttu-id="29cc3-103">Enable Azure Active Directory authentication for the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="29cc3-103">Enable Azure Active Directory authentication for the Azure-SSIS integration runtime</span></span>

<span data-ttu-id="29cc3-104">This article shows you how to create an Azure-SSIS IR with Azure Data Factory service identity.</span><span class="sxs-lookup"><span data-stu-id="29cc3-104">This article shows you how to create an Azure-SSIS IR with Azure Data Factory service identity.</span></span> <span data-ttu-id="29cc3-105">Azure Active Directory (Azure AD) authentication with the Managed Service Identity (MSI) for the Azure-SSIS integration runtime lets you use the Data Factory MSI instead of SQL authentication to create an Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="29cc3-105">Azure Active Directory (Azure AD) authentication with the Managed Service Identity (MSI) for the Azure-SSIS integration runtime lets you use the Data Factory MSI instead of SQL authentication to create an Azure-SSIS integration runtime.</span></span>

<span data-ttu-id="29cc3-106">For more info about the Data Factory MSI, see [Azure Data Factory service identity](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-service-identity).</span><span class="sxs-lookup"><span data-stu-id="29cc3-106">For more info about the Data Factory MSI, see [Azure Data Factory service identity](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-service-identity).</span></span>

> [!NOTE]
> <span data-ttu-id="29cc3-107">If you have already created an Azure-SSIS integration runtime with SQL authentication, you can't reconfigure the IR to use Azure AD authentication with PowerShell at this time.</span><span class="sxs-lookup"><span data-stu-id="29cc3-107">If you have already created an Azure-SSIS integration runtime with SQL authentication, you can't reconfigure the IR to use Azure AD authentication with PowerShell at this time.</span></span>

## <a name="create-a-group-in-azure-ad-and-make-the-data-factory-msi-a-member-of-the-group"></a><span data-ttu-id="29cc3-108">Create a group in Azure AD and make the Data Factory MSI a member of the group</span><span class="sxs-lookup"><span data-stu-id="29cc3-108">Create a group in Azure AD and make the Data Factory MSI a member of the group</span></span>

<span data-ttu-id="29cc3-109">You can use an existing Azure AD group, or create a new one using Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29cc3-109">You can use an existing Azure AD group, or create a new one using Azure AD PowerShell.</span></span>

1.  <span data-ttu-id="29cc3-110">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span><span class="sxs-lookup"><span data-stu-id="29cc3-110">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span></span>

2.  <span data-ttu-id="29cc3-111">Sign in using `Connect-AzureAD`, and run the following command to create the group, and save it in a variable:</span><span class="sxs-lookup"><span data-stu-id="29cc3-111">Sign in using `Connect-AzureAD`, and run the following command to create the group, and save it in a variable:</span></span>

    ```powershell
    $Group = New-AzureADGroup -DisplayName "SSISIrGroup" `
                              -MailEnabled $false `
                              -SecurityEnabled $true `
                              -MailNickName "NotSet"
    ```

    <span data-ttu-id="29cc3-112">The output looks like the following example, which also examines the value of the variable:</span><span class="sxs-lookup"><span data-stu-id="29cc3-112">The output looks like the following example, which also examines the value of the variable:</span></span>

    ```powershell
    $Group

    ObjectId DisplayName Description
    -------- ----------- -----------
    6de75f3c-8b2f-4bf4-b9f8-78cc60a18050 SSISIrGroup
    ```

3.  <span data-ttu-id="29cc3-113">Add the Data Factory MSI to the group.</span><span class="sxs-lookup"><span data-stu-id="29cc3-113">Add the Data Factory MSI to the group.</span></span> <span data-ttu-id="29cc3-114">You can follow [Azure Data Factory service identity](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-service-identity) to get the principal SERVICE IDENTITY ID (for example, 765ad4ab-XXXX-XXXX-XXXX-51ed985819dc, but do not use SERVICE IDENTITY APPLICATION ID for this purpose).</span><span class="sxs-lookup"><span data-stu-id="29cc3-114">You can follow [Azure Data Factory service identity](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-service-identity) to get the principal SERVICE IDENTITY ID (for example, 765ad4ab-XXXX-XXXX-XXXX-51ed985819dc, but do not use SERVICE IDENTITY APPLICATION ID for this purpose).</span></span>

    ```powershell
    Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId 765ad4ab-XXXX-XXXX-XXXX-51ed985819dc
    ```

    <span data-ttu-id="29cc3-115">You also can examine the group membership afterward.</span><span class="sxs-lookup"><span data-stu-id="29cc3-115">You also can examine the group membership afterward.</span></span>

    ```powershell
    Get-AzureAdGroupMember -ObjectId $Group.ObjectId
    ```

## <a name="enable-azure-ad-on-azure-sql-database"></a><span data-ttu-id="29cc3-116">Enable Azure AD on Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="29cc3-116">Enable Azure AD on Azure SQL Database</span></span>

<span data-ttu-id="29cc3-117">Azure SQL Database supports creating a database with an Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="29cc3-117">Azure SQL Database supports creating a database with an Azure AD user.</span></span> <span data-ttu-id="29cc3-118">As a result, you can set an Azure AD user as the Active Directory admin, and then log in to SSMS using the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="29cc3-118">As a result, you can set an Azure AD user as the Active Directory admin, and then log in to SSMS using the Azure AD user.</span></span> <span data-ttu-id="29cc3-119">Then you can create a contained user for the Azure AD group to enable the IR to create the SQL Server Integration Services (SSIS) catalog on the server.</span><span class="sxs-lookup"><span data-stu-id="29cc3-119">Then you can create a contained user for the Azure AD group to enable the IR to create the SQL Server Integration Services (SSIS) catalog on the server.</span></span>

### <a name="enable-azure-ad-authentication-for-the-azure-sql-database"></a><span data-ttu-id="29cc3-120">Enable Azure AD authentication for the Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="29cc3-120">Enable Azure AD authentication for the Azure SQL Database</span></span>

<span data-ttu-id="29cc3-121">You can [configure Azure AD authentication for the SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) using the following steps:</span><span class="sxs-lookup"><span data-stu-id="29cc3-121">You can [configure Azure AD authentication for the SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) using the following steps:</span></span>

1.  <span data-ttu-id="29cc3-122">In the Azure portal, select **All services** -> **SQL servers** from the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="29cc3-122">In the Azure portal, select **All services** -> **SQL servers** from the left-hand navigation.</span></span>

2.  <span data-ttu-id="29cc3-123">Select the SQL Database to be enabled for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="29cc3-123">Select the SQL Database to be enabled for Azure AD authentication.</span></span>

3.  <span data-ttu-id="29cc3-124">In the **Settings** section of the blade, select **Active Directory admin**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-124">In the **Settings** section of the blade, select **Active Directory admin**.</span></span>

4.  <span data-ttu-id="29cc3-125">In the command bar, select **Set admin**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-125">In the command bar, select **Set admin**.</span></span>

5.  <span data-ttu-id="29cc3-126">Select an Azure AD user account to be made an administrator of the server, and then select **Select.**</span><span class="sxs-lookup"><span data-stu-id="29cc3-126">Select an Azure AD user account to be made an administrator of the server, and then select **Select.**</span></span>

6.  <span data-ttu-id="29cc3-127">In the command bar, select **Save.**</span><span class="sxs-lookup"><span data-stu-id="29cc3-127">In the command bar, select **Save.**</span></span>

### <a name="create-a-contained-user-in-the-database-that-represents-the-azure-ad-group"></a><span data-ttu-id="29cc3-128">Create a contained user in the database that represents the Azure AD group</span><span class="sxs-lookup"><span data-stu-id="29cc3-128">Create a contained user in the database that represents the Azure AD group</span></span>

<span data-ttu-id="29cc3-129">For this next step, you need [Microsoft SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="29cc3-129">For this next step, you need [Microsoft SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span>

1.  <span data-ttu-id="29cc3-130">Start SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="29cc3-130">Start SQL Server Management Studio.</span></span>

2.  <span data-ttu-id="29cc3-131">In the **Connect to Server** dialog, enter your SQL server name in the **Server name** field.</span><span class="sxs-lookup"><span data-stu-id="29cc3-131">In the **Connect to Server** dialog, enter your SQL server name in the **Server name** field.</span></span>

3.  <span data-ttu-id="29cc3-132">In the **Authentication** field, select **Active Directory - Universal with MFA support**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-132">In the **Authentication** field, select **Active Directory - Universal with MFA support**.</span></span> <span data-ttu-id="29cc3-133">(You can also use other two Active Directory authentication types.</span><span class="sxs-lookup"><span data-stu-id="29cc3-133">(You can also use other two Active Directory authentication types.</span></span> <span data-ttu-id="29cc3-134">See [Configure and manage Azure Active Directory authentication with SQL Database, Managed Instance](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure).)</span><span class="sxs-lookup"><span data-stu-id="29cc3-134">See [Configure and manage Azure Active Directory authentication with SQL Database, Managed Instance](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure).)</span></span>

4.  <span data-ttu-id="29cc3-135">In the **User name** field, enter the name of the Azure AD account that you set as the server administrator - for example, testuser@xxxonline.com.</span><span class="sxs-lookup"><span data-stu-id="29cc3-135">In the **User name** field, enter the name of the Azure AD account that you set as the server administrator - for example, testuser@xxxonline.com.</span></span>

5.  <span data-ttu-id="29cc3-136">select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-136">select **Connect**.</span></span> <span data-ttu-id="29cc3-137">Complete the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="29cc3-137">Complete the sign-in process.</span></span>

6.  <span data-ttu-id="29cc3-138">In the **Object Explorer**, expand the **Databases** -> System Databases folder.</span><span class="sxs-lookup"><span data-stu-id="29cc3-138">In the **Object Explorer**, expand the **Databases** -> System Databases folder.</span></span>

7.  <span data-ttu-id="29cc3-139">Right-Select on **master** database and select **New query**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-139">Right-Select on **master** database and select **New query**.</span></span>

8.  <span data-ttu-id="29cc3-140">In the query window, enter the following line, and select **Execute** in the toolbar:</span><span class="sxs-lookup"><span data-stu-id="29cc3-140">In the query window, enter the following line, and select **Execute** in the toolbar:</span></span>

    ```sql
    CREATE USER [SSISIrGroup] FROM EXTERNAL PROVIDER
    ```

    <span data-ttu-id="29cc3-141">The command should complete successfully, creating the contained user for the group.</span><span class="sxs-lookup"><span data-stu-id="29cc3-141">The command should complete successfully, creating the contained user for the group.</span></span>

9.  <span data-ttu-id="29cc3-142">Clear the query window, enter the following line, and Select **Execute** in the toolbar:</span><span class="sxs-lookup"><span data-stu-id="29cc3-142">Clear the query window, enter the following line, and Select **Execute** in the toolbar:</span></span>

    ```sql
    ALTER ROLE dbmanager ADD MEMBER [SSISIrGroup]
    ```

    <span data-ttu-id="29cc3-143">The command should complete successfully, granting the contained user the ability to create database.</span><span class="sxs-lookup"><span data-stu-id="29cc3-143">The command should complete successfully, granting the contained user the ability to create database.</span></span>

## <a name="enable-azure-ad-on-azure-sql-database-managed-instance"></a><span data-ttu-id="29cc3-144">Enable Azure AD on Azure SQL Database Managed Instance</span><span class="sxs-lookup"><span data-stu-id="29cc3-144">Enable Azure AD on Azure SQL Database Managed Instance</span></span>

<span data-ttu-id="29cc3-145">Azure SQL Database Managed Instance doesn't support creating a database with any Azure AD user other than AD admin. As a result, you have to set the Azure AD Group as the Active Directory admin. You don't need to create the contained user.</span><span class="sxs-lookup"><span data-stu-id="29cc3-145">Azure SQL Database Managed Instance doesn't support creating a database with any Azure AD user other than AD admin. As a result, you have to set the Azure AD Group as the Active Directory admin. You don't need to create the contained user.</span></span>

<span data-ttu-id="29cc3-146">You can [configure Azure AD authentication for the SQL Database Managed Instance server](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) using the following steps:</span><span class="sxs-lookup"><span data-stu-id="29cc3-146">You can [configure Azure AD authentication for the SQL Database Managed Instance server](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) using the following steps:</span></span>

7.  <span data-ttu-id="29cc3-147">In the Azure portal, select **All services** -> **SQL servers** from the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="29cc3-147">In the Azure portal, select **All services** -> **SQL servers** from the left-hand navigation.</span></span>

8.  <span data-ttu-id="29cc3-148">Select the SQL server to be enabled for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="29cc3-148">Select the SQL server to be enabled for Azure AD authentication.</span></span>

9.  <span data-ttu-id="29cc3-149">In the **Settings** section of the blade, select **Active Directory admin**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-149">In the **Settings** section of the blade, select **Active Directory admin**.</span></span>

10. <span data-ttu-id="29cc3-150">In the command bar, select **Set admin**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-150">In the command bar, select **Set admin**.</span></span>

11. <span data-ttu-id="29cc3-151">Search and select the Azure AD Group (for example, SSISIrGroup), and select **Select.**</span><span class="sxs-lookup"><span data-stu-id="29cc3-151">Search and select the Azure AD Group (for example, SSISIrGroup), and select **Select.**</span></span>

12. <span data-ttu-id="29cc3-152">In the command bar, select **Save.**</span><span class="sxs-lookup"><span data-stu-id="29cc3-152">In the command bar, select **Save.**</span></span>

## <a name="provision-the-azure-ssis-ir-in-the-portal"></a><span data-ttu-id="29cc3-153">Provision the Azure-SSIS IR in the portal</span><span class="sxs-lookup"><span data-stu-id="29cc3-153">Provision the Azure-SSIS IR in the portal</span></span>

<span data-ttu-id="29cc3-154">When you provision your Azure-SSIS IR with the Azure portal, on the **SQL Settings** page, check the "Use AAD authentication with your ADF MSI" option.</span><span class="sxs-lookup"><span data-stu-id="29cc3-154">When you provision your Azure-SSIS IR with the Azure portal, on the **SQL Settings** page, check the "Use AAD authentication with your ADF MSI" option.</span></span> <span data-ttu-id="29cc3-155">(The following screenshot shows the settings for IR with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="29cc3-155">(The following screenshot shows the settings for IR with Azure SQL Database.</span></span> <span data-ttu-id="29cc3-156">For the IR with Managed Instance, the "Catalog Database Service Tier" property is not available; other settings are the same.)</span><span class="sxs-lookup"><span data-stu-id="29cc3-156">For the IR with Managed Instance, the "Catalog Database Service Tier" property is not available; other settings are the same.)</span></span>

<span data-ttu-id="29cc3-157">For more info about how to create an Azure-SSIS integration runtime, see [Create an Azure-SSIS integration runtime in Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="29cc3-157">For more info about how to create an Azure-SSIS integration runtime, see [Create an Azure-SSIS integration runtime in Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span></span>

![Settings for the Azure-SSIS integration runtime](media/enable-aad-authentication-azure-ssis-ir/enable-aad-authentication.png)

## <a name="provision-the-azure-ssis-ir-with-powershell"></a><span data-ttu-id="29cc3-159">Provision the Azure-SSIS IR with PowerShell</span><span class="sxs-lookup"><span data-stu-id="29cc3-159">Provision the Azure-SSIS IR with PowerShell</span></span>

<span data-ttu-id="29cc3-160">To provision your Azure-SSIS IR with PowerShell, do the following things:</span><span class="sxs-lookup"><span data-stu-id="29cc3-160">To provision your Azure-SSIS IR with PowerShell, do the following things:</span></span>

1.  <span data-ttu-id="29cc3-161">Install the [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/tag/v5.5.0-March2018) module.</span><span class="sxs-lookup"><span data-stu-id="29cc3-161">Install the [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/tag/v5.5.0-March2018) module.</span></span>

2.  <span data-ttu-id="29cc3-162">In your script, do not set the *CatalogAdminCredential* parameter.</span><span class="sxs-lookup"><span data-stu-id="29cc3-162">In your script, do not set the *CatalogAdminCredential* parameter.</span></span> <span data-ttu-id="29cc3-163">For example:</span><span class="sxs-lookup"><span data-stu-id="29cc3-163">For example:</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                               -DataFactoryName $DataFactoryName `
                                               -Name $AzureSSISName `
                                               -Type Managed `
                                               -CatalogServerEndpoint $SSISDBServerEndpoint `
                                               -CatalogPricingTier $SSISDBPricingTier `
                                               -Description $AzureSSISDescription `
                                               -Edition $AzureSSISEdition `
                                               -Location $AzureSSISLocation `
                                               -NodeSize $AzureSSISNodeSize `
                                               -NodeCount $AzureSSISNodeNumber `
                                               -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                               -SetupScriptContainerSasUri $SetupScriptContainerSasUri

    Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                                 -DataFactoryName $DataFactoryName `
                                                 -Name $AzureSSISName
   ```
