---
title: Copy data to or from Azure SQL Database by using Data Factory | Microsoft Docs
description: Learn how to copy data from supported source data stores to Azure SQL Database or from SQL Database to supported sink data stores by using Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/05/2018
ms.author: jingwang
ms.openlocfilehash: afb4cbafeb29800b1f5b1c837da301e2944d678b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865631"
---
# <a name="copy-data-to-or-from-azure-sql-database-by-using-azure-data-factory"></a><span data-ttu-id="15a09-103">Copy data to or from Azure SQL Database by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="15a09-103">Copy data to or from Azure SQL Database by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you use:"]
> * [Version 1](v1/data-factory-azure-sql-connector.md)
> * [Current version](connector-azure-sql-database.md)

<span data-ttu-id="15a09-106">This article explains how to use Copy Activity in Azure Data Factory to copy data from or to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="15a09-106">This article explains how to use Copy Activity in Azure Data Factory to copy data from or to Azure SQL Database.</span></span> <span data-ttu-id="15a09-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article, which presents a general overview of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="15a09-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article, which presents a general overview of Copy Activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="15a09-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="15a09-108">Supported capabilities</span></span>

<span data-ttu-id="15a09-109">You can copy data from or to Azure SQL Database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="15a09-109">You can copy data from or to Azure SQL Database to any supported sink data store.</span></span> <span data-ttu-id="15a09-110">And you can copy data from any supported source data store to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="15a09-110">And you can copy data from any supported source data store to Azure SQL Database.</span></span> <span data-ttu-id="15a09-111">For a list of data stores that are supported as sources or sinks by Copy Activity, see the [Supported data stores and formats](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="15a09-111">For a list of data stores that are supported as sources or sinks by Copy Activity, see the [Supported data stores and formats](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="15a09-112">Specifically, this Azure SQL Database connector supports these functions:</span><span class="sxs-lookup"><span data-stu-id="15a09-112">Specifically, this Azure SQL Database connector supports these functions:</span></span>

- <span data-ttu-id="15a09-113">Copy data by using SQL authentication and Azure Active Directory (Azure AD) Application token authentication with a service principal or Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="15a09-113">Copy data by using SQL authentication and Azure Active Directory (Azure AD) Application token authentication with a service principal or Managed Service Identity (MSI).</span></span>
- <span data-ttu-id="15a09-114">As a source, retrieve data by using a SQL query or stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-114">As a source, retrieve data by using a SQL query or stored procedure.</span></span>
- <span data-ttu-id="15a09-115">As a sink, append data to a destination table or invoke a stored procedure with custom logic during the copy.</span><span class="sxs-lookup"><span data-stu-id="15a09-115">As a sink, append data to a destination table or invoke a stored procedure with custom logic during the copy.</span></span>

> [!IMPORTANT]
> If you copy data by using Azure Data Factory Integration Runtime, configure an [Azure SQL server firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) so that Azure Services can access the server.
> If you copy data by using a self-hosted integration runtime, configure the Azure SQL server firewall to allow the appropriate IP range. This range includes the machine's IP that is used to connect to Azure SQL Database.

## <a name="get-started"></a><span data-ttu-id="15a09-119">Get started</span><span class="sxs-lookup"><span data-stu-id="15a09-119">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="15a09-120">The following sections provide details about properties that are used to define Data Factory entities specific to an Azure SQL Database connector.</span><span class="sxs-lookup"><span data-stu-id="15a09-120">The following sections provide details about properties that are used to define Data Factory entities specific to an Azure SQL Database connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="15a09-121">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="15a09-121">Linked service properties</span></span>

<span data-ttu-id="15a09-122">These properties are supported for an Azure SQL Database linked service:</span><span class="sxs-lookup"><span data-stu-id="15a09-122">These properties are supported for an Azure SQL Database linked service:</span></span>

| <span data-ttu-id="15a09-123">Property</span><span class="sxs-lookup"><span data-stu-id="15a09-123">Property</span></span> | <span data-ttu-id="15a09-124">Description</span><span class="sxs-lookup"><span data-stu-id="15a09-124">Description</span></span> | <span data-ttu-id="15a09-125">Required</span><span class="sxs-lookup"><span data-stu-id="15a09-125">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="15a09-126">type</span><span class="sxs-lookup"><span data-stu-id="15a09-126">type</span></span> | <span data-ttu-id="15a09-127">The **type** property must be set to **AzureSqlDatabase**.</span><span class="sxs-lookup"><span data-stu-id="15a09-127">The **type** property must be set to **AzureSqlDatabase**.</span></span> | <span data-ttu-id="15a09-128">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-128">Yes</span></span> |
| <span data-ttu-id="15a09-129">connectionString</span><span class="sxs-lookup"><span data-stu-id="15a09-129">connectionString</span></span> | <span data-ttu-id="15a09-130">Specify information needed to connect to the Azure SQL Database instance for the **connectionString** property.</span><span class="sxs-lookup"><span data-stu-id="15a09-130">Specify information needed to connect to the Azure SQL Database instance for the **connectionString** property.</span></span> <span data-ttu-id="15a09-131">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="15a09-131">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="15a09-132">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-132">Yes</span></span> |
| <span data-ttu-id="15a09-133">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="15a09-133">servicePrincipalId</span></span> | <span data-ttu-id="15a09-134">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="15a09-134">Specify the application's client ID.</span></span> | <span data-ttu-id="15a09-135">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-135">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="15a09-136">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="15a09-136">servicePrincipalKey</span></span> | <span data-ttu-id="15a09-137">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="15a09-137">Specify the application's key.</span></span> <span data-ttu-id="15a09-138">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="15a09-138">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="15a09-139">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-139">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="15a09-140">tenant</span><span class="sxs-lookup"><span data-stu-id="15a09-140">tenant</span></span> | <span data-ttu-id="15a09-141">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="15a09-141">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="15a09-142">Retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15a09-142">Retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="15a09-143">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-143">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="15a09-144">connectVia</span><span class="sxs-lookup"><span data-stu-id="15a09-144">connectVia</span></span> | <span data-ttu-id="15a09-145">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="15a09-145">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="15a09-146">You can use Azure Integration Runtime or a self-hosted integration runtime if your data store is located in a private network.</span><span class="sxs-lookup"><span data-stu-id="15a09-146">You can use Azure Integration Runtime or a self-hosted integration runtime if your data store is located in a private network.</span></span> <span data-ttu-id="15a09-147">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="15a09-147">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="15a09-148">No</span><span class="sxs-lookup"><span data-stu-id="15a09-148">No</span></span> |

<span data-ttu-id="15a09-149">For different authentication types, refer to the following sections on prerequisites and JSON samples, respectively:</span><span class="sxs-lookup"><span data-stu-id="15a09-149">For different authentication types, refer to the following sections on prerequisites and JSON samples, respectively:</span></span>

- [<span data-ttu-id="15a09-150">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-150">SQL authentication</span></span>](#sql-authentication)
- [<span data-ttu-id="15a09-151">Azure AD application token authentication: Service principal</span><span class="sxs-lookup"><span data-stu-id="15a09-151">Azure AD application token authentication: Service principal</span></span>](#service-principal-authentication)
- [<span data-ttu-id="15a09-152">Azure AD application token authentication: Managed Service Identity</span><span class="sxs-lookup"><span data-stu-id="15a09-152">Azure AD application token authentication: Managed Service Identity</span></span>](#managed-service-identity-authentication)

>[!TIP]
>If you hit error with error code as "UserErrorFailedToConnectToSqlServer" and message like "The session limit for the database is XXX and has been reached.", add `Pooling=false` to your connection string and try again.

### <a name="sql-authentication"></a><span data-ttu-id="15a09-154">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-154">SQL authentication</span></span>

#### <a name="linked-service-example-that-uses-sql-authentication"></a><span data-ttu-id="15a09-155">Linked service example that uses SQL authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-155">Linked service example that uses SQL authentication</span></span>

```json
{
    "name": "AzureSqlDbLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="service-principal-authentication"></a><span data-ttu-id="15a09-156">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-156">Service principal authentication</span></span>

<span data-ttu-id="15a09-157">To use a service principal-based Azure AD application token authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="15a09-157">To use a service principal-based Azure AD application token authentication, follow these steps:</span></span>

1. <span data-ttu-id="15a09-158">**[Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)** from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15a09-158">**[Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)** from the Azure portal.</span></span> <span data-ttu-id="15a09-159">Make note of the application name and the following values that define the linked service:</span><span class="sxs-lookup"><span data-stu-id="15a09-159">Make note of the application name and the following values that define the linked service:</span></span>

    - <span data-ttu-id="15a09-160">Application ID</span><span class="sxs-lookup"><span data-stu-id="15a09-160">Application ID</span></span>
    - <span data-ttu-id="15a09-161">Application key</span><span class="sxs-lookup"><span data-stu-id="15a09-161">Application key</span></span>
    - <span data-ttu-id="15a09-162">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="15a09-162">Tenant ID</span></span>

1. <span data-ttu-id="15a09-163">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="15a09-163">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span></span> <span data-ttu-id="15a09-164">The Azure AD administrator must be an Azure AD user or Azure AD group, but it can't be a service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-164">The Azure AD administrator must be an Azure AD user or Azure AD group, but it can't be a service principal.</span></span> <span data-ttu-id="15a09-165">This step is done so that, in the next step, you can use an Azure AD identity to create a contained database user for the service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-165">This step is done so that, in the next step, you can use an Azure AD identity to create a contained database user for the service principal.</span></span>

1. <span data-ttu-id="15a09-166">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the service principal.</span><span class="sxs-lookup"><span data-stu-id="15a09-166">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the service principal.</span></span> <span data-ttu-id="15a09-167">Connect to the database from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span><span class="sxs-lookup"><span data-stu-id="15a09-167">Connect to the database from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span></span> <span data-ttu-id="15a09-168">Run the following T-SQL:</span><span class="sxs-lookup"><span data-stu-id="15a09-168">Run the following T-SQL:</span></span> 
    
    ```sql
    CREATE USER [your application name] FROM EXTERNAL PROVIDER;
    ```

1. <span data-ttu-id="15a09-169">**Grant the service principal needed permissions** as you normally do for SQL users or others.</span><span class="sxs-lookup"><span data-stu-id="15a09-169">**Grant the service principal needed permissions** as you normally do for SQL users or others.</span></span> <span data-ttu-id="15a09-170">Run the following code:</span><span class="sxs-lookup"><span data-stu-id="15a09-170">Run the following code:</span></span>

    ```sql
    EXEC sp_addrolemember [role name], [your application name];
    ```

1. <span data-ttu-id="15a09-171">**Configure an Azure SQL Database linked service** in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="15a09-171">**Configure an Azure SQL Database linked service** in Azure Data Factory.</span></span>


#### <a name="linked-service-example-that-uses-service-principal-authentication"></a><span data-ttu-id="15a09-172">Linked service example that uses service principal authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-172">Linked service example that uses service principal authentication</span></span>

```json
{
    "name": "AzureSqlDbLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;Connection Timeout=30"
            },
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": {
                "type": "SecureString",
                "value": "<service principal key>"
            },
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="managed-service-identity-authentication"></a><span data-ttu-id="15a09-173">Managed Service Identity authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-173">Managed Service Identity authentication</span></span>

<span data-ttu-id="15a09-174">A data factory can be associated with a [Managed Service Identity](data-factory-service-identity.md) that represents the specific data factory.</span><span class="sxs-lookup"><span data-stu-id="15a09-174">A data factory can be associated with a [Managed Service Identity](data-factory-service-identity.md) that represents the specific data factory.</span></span> <span data-ttu-id="15a09-175">You can use this service identity for Azure SQL Database authentication.</span><span class="sxs-lookup"><span data-stu-id="15a09-175">You can use this service identity for Azure SQL Database authentication.</span></span> <span data-ttu-id="15a09-176">The designated factory can access and copy data from or to your database by using this identity.</span><span class="sxs-lookup"><span data-stu-id="15a09-176">The designated factory can access and copy data from or to your database by using this identity.</span></span>

<span data-ttu-id="15a09-177">To use MSI-based Azure AD application token authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="15a09-177">To use MSI-based Azure AD application token authentication, follow these steps:</span></span>

1. <span data-ttu-id="15a09-178">**Create a group in Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="15a09-178">**Create a group in Azure AD.**</span></span> <span data-ttu-id="15a09-179">Make the factory MSI a member of the group.</span><span class="sxs-lookup"><span data-stu-id="15a09-179">Make the factory MSI a member of the group.</span></span>
    
    1. <span data-ttu-id="15a09-180">Find the data factory service identity from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15a09-180">Find the data factory service identity from the Azure portal.</span></span> <span data-ttu-id="15a09-181">Go to your data factory's **Properties**.</span><span class="sxs-lookup"><span data-stu-id="15a09-181">Go to your data factory's **Properties**.</span></span> <span data-ttu-id="15a09-182">Copy the SERVICE IDENTITY ID.</span><span class="sxs-lookup"><span data-stu-id="15a09-182">Copy the SERVICE IDENTITY ID.</span></span>
    
    1. <span data-ttu-id="15a09-183">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span><span class="sxs-lookup"><span data-stu-id="15a09-183">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span></span> <span data-ttu-id="15a09-184">Sign in by using the `Connect-AzureAD` command.</span><span class="sxs-lookup"><span data-stu-id="15a09-184">Sign in by using the `Connect-AzureAD` command.</span></span> <span data-ttu-id="15a09-185">Run the following commands to create a group and add the data factory MSI as a member.</span><span class="sxs-lookup"><span data-stu-id="15a09-185">Run the following commands to create a group and add the data factory MSI as a member.</span></span>
    ```powershell
    $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
    Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory service identity ID>"
    ```
    
1. <span data-ttu-id="15a09-186">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="15a09-186">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span></span> <span data-ttu-id="15a09-187">The Azure AD administrator can be an Azure AD user or Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="15a09-187">The Azure AD administrator can be an Azure AD user or Azure AD group.</span></span> <span data-ttu-id="15a09-188">If you grant the group with MSI an admin role, skip steps 3 and 4.</span><span class="sxs-lookup"><span data-stu-id="15a09-188">If you grant the group with MSI an admin role, skip steps 3 and 4.</span></span> <span data-ttu-id="15a09-189">The administrator will have full access to the database.</span><span class="sxs-lookup"><span data-stu-id="15a09-189">The administrator will have full access to the database.</span></span>

1. <span data-ttu-id="15a09-190">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="15a09-190">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the Azure AD group.</span></span> <span data-ttu-id="15a09-191">Connect to the database from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span><span class="sxs-lookup"><span data-stu-id="15a09-191">Connect to the database from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span></span> <span data-ttu-id="15a09-192">Run the following T-SQL:</span><span class="sxs-lookup"><span data-stu-id="15a09-192">Run the following T-SQL:</span></span> 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. <span data-ttu-id="15a09-193">**Grant the Azure AD group needed permissions** as you normally do for SQL users and others.</span><span class="sxs-lookup"><span data-stu-id="15a09-193">**Grant the Azure AD group needed permissions** as you normally do for SQL users and others.</span></span> <span data-ttu-id="15a09-194">For example, run the following code:</span><span class="sxs-lookup"><span data-stu-id="15a09-194">For example, run the following code:</span></span>

    ```sql
    EXEC sp_addrolemember [role name], [your AAD group name];
    ```

1. <span data-ttu-id="15a09-195">**Configure an Azure SQL Database linked service** in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="15a09-195">**Configure an Azure SQL Database linked service** in Azure Data Factory.</span></span>

#### <a name="linked-service-example-that-uses-msi-authentication"></a><span data-ttu-id="15a09-196">Linked service example that uses MSI authentication</span><span class="sxs-lookup"><span data-stu-id="15a09-196">Linked service example that uses MSI authentication</span></span>

```json
{
    "name": "AzureSqlDbLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;Connection Timeout=30"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="15a09-197">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="15a09-197">Dataset properties</span></span>

<span data-ttu-id="15a09-198">For a full list of sections and properties available for defining datasets, see the [Datasets](https://docs.microsoft.com/en-us/azure/data-factory/concepts-datasets-linked-services) article.</span><span class="sxs-lookup"><span data-stu-id="15a09-198">For a full list of sections and properties available for defining datasets, see the [Datasets](https://docs.microsoft.com/en-us/azure/data-factory/concepts-datasets-linked-services) article.</span></span> <span data-ttu-id="15a09-199">This section provides a list of properties supported by the Azure SQL Database dataset.</span><span class="sxs-lookup"><span data-stu-id="15a09-199">This section provides a list of properties supported by the Azure SQL Database dataset.</span></span>

<span data-ttu-id="15a09-200">To copy data from or to Azure SQL Database, set the **type** property of the dataset to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="15a09-200">To copy data from or to Azure SQL Database, set the **type** property of the dataset to **AzureSqlTable**.</span></span> <span data-ttu-id="15a09-201">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="15a09-201">The following properties are supported:</span></span>

| <span data-ttu-id="15a09-202">Property</span><span class="sxs-lookup"><span data-stu-id="15a09-202">Property</span></span> | <span data-ttu-id="15a09-203">Description</span><span class="sxs-lookup"><span data-stu-id="15a09-203">Description</span></span> | <span data-ttu-id="15a09-204">Required</span><span class="sxs-lookup"><span data-stu-id="15a09-204">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="15a09-205">type</span><span class="sxs-lookup"><span data-stu-id="15a09-205">type</span></span> | <span data-ttu-id="15a09-206">The **type** property of the dataset must be set to **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="15a09-206">The **type** property of the dataset must be set to **AzureSqlTable**.</span></span> | <span data-ttu-id="15a09-207">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-207">Yes</span></span> |
| <span data-ttu-id="15a09-208">tableName</span><span class="sxs-lookup"><span data-stu-id="15a09-208">tableName</span></span> | <span data-ttu-id="15a09-209">The name of the table or view in the Azure SQL Database instance that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="15a09-209">The name of the table or view in the Azure SQL Database instance that the linked service refers to.</span></span> | <span data-ttu-id="15a09-210">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-210">Yes</span></span> |

#### <a name="dataset-properties-example"></a><span data-ttu-id="15a09-211">Dataset properties example</span><span class="sxs-lookup"><span data-stu-id="15a09-211">Dataset properties example</span></span>

```json
{
    "name": "AzureSQLDbDataset",
    "properties":
    {
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Database linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="15a09-212">Copy Activity properties</span><span class="sxs-lookup"><span data-stu-id="15a09-212">Copy Activity properties</span></span>

<span data-ttu-id="15a09-213">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="15a09-213">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="15a09-214">This section provides a list of properties supported by the Azure SQL Database source and sink.</span><span class="sxs-lookup"><span data-stu-id="15a09-214">This section provides a list of properties supported by the Azure SQL Database source and sink.</span></span>

### <a name="azure-sql-database-as-the-source"></a><span data-ttu-id="15a09-215">Azure SQL Database as the source</span><span class="sxs-lookup"><span data-stu-id="15a09-215">Azure SQL Database as the source</span></span>

<span data-ttu-id="15a09-216">To copy data from Azure SQL Database, set the **type** property in the Copy Activity source to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="15a09-216">To copy data from Azure SQL Database, set the **type** property in the Copy Activity source to **SqlSource**.</span></span> <span data-ttu-id="15a09-217">The following properties are supported in the Copy Activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="15a09-217">The following properties are supported in the Copy Activity **source** section:</span></span>

| <span data-ttu-id="15a09-218">Property</span><span class="sxs-lookup"><span data-stu-id="15a09-218">Property</span></span> | <span data-ttu-id="15a09-219">Description</span><span class="sxs-lookup"><span data-stu-id="15a09-219">Description</span></span> | <span data-ttu-id="15a09-220">Required</span><span class="sxs-lookup"><span data-stu-id="15a09-220">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="15a09-221">type</span><span class="sxs-lookup"><span data-stu-id="15a09-221">type</span></span> | <span data-ttu-id="15a09-222">The **type** property of the Copy Activity source must be set to **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="15a09-222">The **type** property of the Copy Activity source must be set to **SqlSource**.</span></span> | <span data-ttu-id="15a09-223">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-223">Yes</span></span> |
| <span data-ttu-id="15a09-224">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="15a09-224">sqlReaderQuery</span></span> | <span data-ttu-id="15a09-225">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="15a09-225">Use the custom SQL query to read data.</span></span> <span data-ttu-id="15a09-226">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="15a09-226">Example: `select * from MyTable`.</span></span> | <span data-ttu-id="15a09-227">No</span><span class="sxs-lookup"><span data-stu-id="15a09-227">No</span></span> |
| <span data-ttu-id="15a09-228">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="15a09-228">sqlReaderStoredProcedureName</span></span> | <span data-ttu-id="15a09-229">The name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="15a09-229">The name of the stored procedure that reads data from the source table.</span></span> <span data-ttu-id="15a09-230">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-230">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> | <span data-ttu-id="15a09-231">No</span><span class="sxs-lookup"><span data-stu-id="15a09-231">No</span></span> |
| <span data-ttu-id="15a09-232">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="15a09-232">storedProcedureParameters</span></span> | <span data-ttu-id="15a09-233">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-233">Parameters for the stored procedure.</span></span><br/><span data-ttu-id="15a09-234">Allowed values are name or value pairs.</span><span class="sxs-lookup"><span data-stu-id="15a09-234">Allowed values are name or value pairs.</span></span> <span data-ttu-id="15a09-235">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="15a09-235">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> | <span data-ttu-id="15a09-236">No</span><span class="sxs-lookup"><span data-stu-id="15a09-236">No</span></span> |

### <a name="points-to-note"></a><span data-ttu-id="15a09-237">Points to note</span><span class="sxs-lookup"><span data-stu-id="15a09-237">Points to note</span></span>

- <span data-ttu-id="15a09-238">If the **sqlReaderQuery** is specified for the **SqlSource**, Copy Activity runs this query against the Azure SQL Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="15a09-238">If the **sqlReaderQuery** is specified for the **SqlSource**, Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="15a09-239">Or you can specify a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-239">Or you can specify a stored procedure.</span></span> <span data-ttu-id="15a09-240">Specify **sqlReaderStoredProcedureName** and **storedProcedureParameters** if the stored procedure takes parameters.</span><span class="sxs-lookup"><span data-stu-id="15a09-240">Specify **sqlReaderStoredProcedureName** and **storedProcedureParameters** if the stored procedure takes parameters.</span></span>
- <span data-ttu-id="15a09-241">If you don't specify either **sqlReaderQuery** or **sqlReaderStoredProcedureName**, the columns defined in the **structure** section of the dataset JSON are used to construct a query.</span><span class="sxs-lookup"><span data-stu-id="15a09-241">If you don't specify either **sqlReaderQuery** or **sqlReaderStoredProcedureName**, the columns defined in the **structure** section of the dataset JSON are used to construct a query.</span></span> <span data-ttu-id="15a09-242">`select column1, column2 from mytable` runs against Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="15a09-242">`select column1, column2 from mytable` runs against Azure SQL Database.</span></span> <span data-ttu-id="15a09-243">If the dataset definition doesn't have the **structure**, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="15a09-243">If the dataset definition doesn't have the **structure**, all columns are selected from the table.</span></span>
- <span data-ttu-id="15a09-244">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="15a09-244">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span></span>

#### <a name="sql-query-example"></a><span data-ttu-id="15a09-245">SQL query example</span><span class="sxs-lookup"><span data-stu-id="15a09-245">SQL query example</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL Database input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
                "sqlReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

#### <a name="stored-procedure-example"></a><span data-ttu-id="15a09-246">Stored procedure example</span><span class="sxs-lookup"><span data-stu-id="15a09-246">Stored procedure example</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL Database input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
                "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
                "storedProcedureParameters": {
                    "stringData": { "value": "str3" },
                    "identifier": { "value": "$$Text.Format('{0:yyyy}', <datetime parameter>)", "type": "Int"}
                }
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="stored-procedure-definition"></a><span data-ttu-id="15a09-247">Stored procedure definition</span><span class="sxs-lookup"><span data-stu-id="15a09-247">Stored procedure definition</span></span>

```sql
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="azure-sql-database-as-the-sink"></a><span data-ttu-id="15a09-248">Azure SQL Database as the sink</span><span class="sxs-lookup"><span data-stu-id="15a09-248">Azure SQL Database as the sink</span></span>

<span data-ttu-id="15a09-249">To copy data to Azure SQL Database, set the **type** property in the Copy Activity sink to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="15a09-249">To copy data to Azure SQL Database, set the **type** property in the Copy Activity sink to **SqlSink**.</span></span> <span data-ttu-id="15a09-250">The following properties are supported in the Copy Activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="15a09-250">The following properties are supported in the Copy Activity **sink** section:</span></span>

| <span data-ttu-id="15a09-251">Property</span><span class="sxs-lookup"><span data-stu-id="15a09-251">Property</span></span> | <span data-ttu-id="15a09-252">Description</span><span class="sxs-lookup"><span data-stu-id="15a09-252">Description</span></span> | <span data-ttu-id="15a09-253">Required</span><span class="sxs-lookup"><span data-stu-id="15a09-253">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="15a09-254">type</span><span class="sxs-lookup"><span data-stu-id="15a09-254">type</span></span> | <span data-ttu-id="15a09-255">The **type** property of the Copy Activity sink must be set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="15a09-255">The **type** property of the Copy Activity sink must be set to **SqlSink**.</span></span> | <span data-ttu-id="15a09-256">Yes</span><span class="sxs-lookup"><span data-stu-id="15a09-256">Yes</span></span> |
| <span data-ttu-id="15a09-257">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="15a09-257">writeBatchSize</span></span> | <span data-ttu-id="15a09-258">Inserts data into the SQL table when the buffer size reaches **writeBatchSize**.</span><span class="sxs-lookup"><span data-stu-id="15a09-258">Inserts data into the SQL table when the buffer size reaches **writeBatchSize**.</span></span><br/> <span data-ttu-id="15a09-259">The allowed value is **integer** (number of rows).</span><span class="sxs-lookup"><span data-stu-id="15a09-259">The allowed value is **integer** (number of rows).</span></span> | <span data-ttu-id="15a09-260">No.</span><span class="sxs-lookup"><span data-stu-id="15a09-260">No.</span></span> <span data-ttu-id="15a09-261">The default is 10000.</span><span class="sxs-lookup"><span data-stu-id="15a09-261">The default is 10000.</span></span> |
| <span data-ttu-id="15a09-262">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="15a09-262">writeBatchTimeout</span></span> | <span data-ttu-id="15a09-263">The wait time for the batch insert operation to finish before it times out.</span><span class="sxs-lookup"><span data-stu-id="15a09-263">The wait time for the batch insert operation to finish before it times out.</span></span><br/> <span data-ttu-id="15a09-264">The allowed value is **timespan**.</span><span class="sxs-lookup"><span data-stu-id="15a09-264">The allowed value is **timespan**.</span></span> <span data-ttu-id="15a09-265">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="15a09-265">Example: “00:30:00” (30 minutes).</span></span> | <span data-ttu-id="15a09-266">No</span><span class="sxs-lookup"><span data-stu-id="15a09-266">No</span></span> |
| <span data-ttu-id="15a09-267">preCopyScript</span><span class="sxs-lookup"><span data-stu-id="15a09-267">preCopyScript</span></span> | <span data-ttu-id="15a09-268">Specify a SQL query for Copy Activity to run before writing data into Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="15a09-268">Specify a SQL query for Copy Activity to run before writing data into Azure SQL Database.</span></span> <span data-ttu-id="15a09-269">It's only invoked once per copy run.</span><span class="sxs-lookup"><span data-stu-id="15a09-269">It's only invoked once per copy run.</span></span> <span data-ttu-id="15a09-270">Use this property to clean up the preloaded data.</span><span class="sxs-lookup"><span data-stu-id="15a09-270">Use this property to clean up the preloaded data.</span></span> | <span data-ttu-id="15a09-271">No</span><span class="sxs-lookup"><span data-stu-id="15a09-271">No</span></span> |
| <span data-ttu-id="15a09-272">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="15a09-272">sqlWriterStoredProcedureName</span></span> | <span data-ttu-id="15a09-273">The name of the stored procedure that defines how to apply source data into a target table.</span><span class="sxs-lookup"><span data-stu-id="15a09-273">The name of the stored procedure that defines how to apply source data into a target table.</span></span> <span data-ttu-id="15a09-274">An example is to do upserts or transform by using your own business logic.</span><span class="sxs-lookup"><span data-stu-id="15a09-274">An example is to do upserts or transform by using your own business logic.</span></span> <br/><br/><span data-ttu-id="15a09-275">This stored procedure is **invoked per batch**.</span><span class="sxs-lookup"><span data-stu-id="15a09-275">This stored procedure is **invoked per batch**.</span></span> <span data-ttu-id="15a09-276">For operations that only run once and have nothing to do with source data, use the `preCopyScript` property.</span><span class="sxs-lookup"><span data-stu-id="15a09-276">For operations that only run once and have nothing to do with source data, use the `preCopyScript` property.</span></span> <span data-ttu-id="15a09-277">Example operations are delete and truncate.</span><span class="sxs-lookup"><span data-stu-id="15a09-277">Example operations are delete and truncate.</span></span> | <span data-ttu-id="15a09-278">No</span><span class="sxs-lookup"><span data-stu-id="15a09-278">No</span></span> |
| <span data-ttu-id="15a09-279">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="15a09-279">storedProcedureParameters</span></span> |<span data-ttu-id="15a09-280">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-280">Parameters for the stored procedure.</span></span><br/><span data-ttu-id="15a09-281">Allowed values are name and value pairs.</span><span class="sxs-lookup"><span data-stu-id="15a09-281">Allowed values are name and value pairs.</span></span> <span data-ttu-id="15a09-282">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="15a09-282">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> | <span data-ttu-id="15a09-283">No</span><span class="sxs-lookup"><span data-stu-id="15a09-283">No</span></span> |
| <span data-ttu-id="15a09-284">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="15a09-284">sqlWriterTableType</span></span> | <span data-ttu-id="15a09-285">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="15a09-285">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="15a09-286">Copy Activity makes the data being moved available in a temporary table with this table type.</span><span class="sxs-lookup"><span data-stu-id="15a09-286">Copy Activity makes the data being moved available in a temporary table with this table type.</span></span> <span data-ttu-id="15a09-287">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="15a09-287">Stored procedure code can then merge the data being copied with existing data.</span></span> | <span data-ttu-id="15a09-288">No</span><span class="sxs-lookup"><span data-stu-id="15a09-288">No</span></span> |

> [!TIP]
> When you copy data to Azure SQL Database, Copy Activity appends data to the sink table by default. To do an upsert or additional business logic, use the stored procedure in **SqlSink**. Learn more details from [Invoking stored procedure from SQL Sink](#invoking-stored-procedure-for-sql-sink).

#### <a name="append-data-example"></a><span data-ttu-id="15a09-292">Append data example</span><span class="sxs-lookup"><span data-stu-id="15a09-292">Append data example</span></span>

```json
"activities":[
    {
        "name": "CopyToAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure SQL Database output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "writeBatchSize": 100000
            }
        }
    }
]
```

#### <a name="invoke-a-stored-procedure-during-copy-for-upsert-example"></a><span data-ttu-id="15a09-293">Invoke a stored procedure during copy for upsert example</span><span class="sxs-lookup"><span data-stu-id="15a09-293">Invoke a stored procedure during copy for upsert example</span></span>

<span data-ttu-id="15a09-294">Learn more details from [Invoking stored procedure from SQL Sink](#invoking-stored-procedure-for-sql-sink).</span><span class="sxs-lookup"><span data-stu-id="15a09-294">Learn more details from [Invoking stored procedure from SQL Sink](#invoking-stored-procedure-for-sql-sink).</span></span>

```json
"activities":[
    {
        "name": "CopyToAzureSQLDatabase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure SQL Database output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SqlSink",
                "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
                "sqlWriterTableType": "CopyTestTableType",
                "storedProcedureParameters": {
                    "identifier": { "value": "1", "type": "Int" },
                    "stringData": { "value": "str1" }
                }
            }
        }
    }
]
```

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="15a09-295">Identity columns in the target database</span><span class="sxs-lookup"><span data-stu-id="15a09-295">Identity columns in the target database</span></span>

<span data-ttu-id="15a09-296">This section shows you how to copy data from a source table without an identity column to a destination table with an identity column.</span><span class="sxs-lookup"><span data-stu-id="15a09-296">This section shows you how to copy data from a source table without an identity column to a destination table with an identity column.</span></span>

#### <a name="source-table"></a><span data-ttu-id="15a09-297">Source table</span><span class="sxs-lookup"><span data-stu-id="15a09-297">Source table</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```

#### <a name="destination-table"></a><span data-ttu-id="15a09-298">Destination table</span><span class="sxs-lookup"><span data-stu-id="15a09-298">Destination table</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

> [!NOTE]
> The target table has an identity column.

#### <a name="source-dataset-json-definition"></a><span data-ttu-id="15a09-300">Source dataset JSON definition</span><span class="sxs-lookup"><span data-stu-id="15a09-300">Source dataset JSON definition</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "type": " AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "SourceTbl"
        }
    }
}
```

#### <a name="destination-dataset-json-definition"></a><span data-ttu-id="15a09-301">Destination dataset JSON definition</span><span class="sxs-lookup"><span data-stu-id="15a09-301">Destination dataset JSON definition</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "TestIdentitySQL",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "TargetTbl"
        }
    }
}
```

> [!NOTE]
> Your source and target table have different schema. 

<span data-ttu-id="15a09-303">The target has an additional column with an identity.</span><span class="sxs-lookup"><span data-stu-id="15a09-303">The target has an additional column with an identity.</span></span> <span data-ttu-id="15a09-304">In this scenario, you must specify the **structure** property in the target dataset definition, which doesn’t include the identity column.</span><span class="sxs-lookup"><span data-stu-id="15a09-304">In this scenario, you must specify the **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoking-stored-procedure-for-sql-sink"></a> <span data-ttu-id="15a09-305">Invoke stored procedure from SQL sink</span><span class="sxs-lookup"><span data-stu-id="15a09-305">Invoke stored procedure from SQL sink</span></span>

<span data-ttu-id="15a09-306">When you copy data into Azure SQL Database, you can also configure and invoke a user-specified stored procedure  with additional parameters.</span><span class="sxs-lookup"><span data-stu-id="15a09-306">When you copy data into Azure SQL Database, you can also configure and invoke a user-specified stored procedure  with additional parameters.</span></span>

<span data-ttu-id="15a09-307">You can use a stored procedure when built-in copy mechanisms don't serve the purpose.</span><span class="sxs-lookup"><span data-stu-id="15a09-307">You can use a stored procedure when built-in copy mechanisms don't serve the purpose.</span></span> <span data-ttu-id="15a09-308">They're typically used when an upsert, insert plus update, or extra processing must be done before the final insertion of source data into the destination table.</span><span class="sxs-lookup"><span data-stu-id="15a09-308">They're typically used when an upsert, insert plus update, or extra processing must be done before the final insertion of source data into the destination table.</span></span> <span data-ttu-id="15a09-309">Some extra processing examples are merge columns, look up additional values, and insertion into more than one table.</span><span class="sxs-lookup"><span data-stu-id="15a09-309">Some extra processing examples are merge columns, look up additional values, and insertion into more than one table.</span></span>

<span data-ttu-id="15a09-310">The following sample shows how to use a stored procedure to do an upsert into a table in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="15a09-310">The following sample shows how to use a stored procedure to do an upsert into a table in Azure SQL Database.</span></span> <span data-ttu-id="15a09-311">Assume that input data and the sink **Marketing** table each have three columns: **ProfileID**, **State**, and **Category**.</span><span class="sxs-lookup"><span data-stu-id="15a09-311">Assume that input data and the sink **Marketing** table each have three columns: **ProfileID**, **State**, and **Category**.</span></span> <span data-ttu-id="15a09-312">Do the upsert based on the **ProfileID** column, and only apply it for a specific category.</span><span class="sxs-lookup"><span data-stu-id="15a09-312">Do the upsert based on the **ProfileID** column, and only apply it for a specific category.</span></span>

#### <a name="output-dataset"></a><span data-ttu-id="15a09-313">Output dataset</span><span class="sxs-lookup"><span data-stu-id="15a09-313">Output dataset</span></span>

```json
{
    "name": "AzureSQLDbDataset",
    "properties":
    {
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Database linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "Marketing"
        }
    }
}
```

<span data-ttu-id="15a09-314">Define the **SqlSink** section in Copy Activity:</span><span class="sxs-lookup"><span data-stu-id="15a09-314">Define the **SqlSink** section in Copy Activity:</span></span>

```json
"sink": {
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing",
    "storedProcedureParameters": {
        "category": {
            "value": "ProductA"
        }
    }
}
```

<span data-ttu-id="15a09-315">In your database, define the stored procedure with the same name as the **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="15a09-315">In your database, define the stored procedure with the same name as the **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="15a09-316">It handles input data from your specified source and merges into the output table.</span><span class="sxs-lookup"><span data-stu-id="15a09-316">It handles input data from your specified source and merges into the output table.</span></span> <span data-ttu-id="15a09-317">The parameter name of the table type in the stored procedure should be the same as the **tableName** defined in the dataset.</span><span class="sxs-lookup"><span data-stu-id="15a09-317">The parameter name of the table type in the stored procedure should be the same as the **tableName** defined in the dataset.</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @category varchar(256)
AS
BEGIN
  MERGE [dbo].[Marketing] AS target
  USING @Marketing AS source
  ON (target.ProfileID = source.ProfileID and target.Category = @category)
  WHEN MATCHED THEN
      UPDATE SET State = source.State
  WHEN NOT MATCHED THEN
      INSERT (ProfileID, State, Category)
      VALUES (source.ProfileID, source.State, source.Category)
END
```

<span data-ttu-id="15a09-318">In your database, define the table type with the same name as the **sqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="15a09-318">In your database, define the table type with the same name as the **sqlWriterTableType**.</span></span> <span data-ttu-id="15a09-319">The schema of the table type should be same as the schema returned by your input data.</span><span class="sxs-lookup"><span data-stu-id="15a09-319">The schema of the table type should be same as the schema returned by your input data.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL,
    [Category] [varchar](256) NOT NULL,
)
```

<span data-ttu-id="15a09-320">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="15a09-320">The stored procedure feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span>

## <a name="data-type-mapping-for-azure-sql-database"></a><span data-ttu-id="15a09-321">Data type mapping for Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="15a09-321">Data type mapping for Azure SQL Database</span></span>

<span data-ttu-id="15a09-322">When you copy data from or to Azure SQL Database, the following mappings are used from Azure SQL Database data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="15a09-322">When you copy data from or to Azure SQL Database, the following mappings are used from Azure SQL Database data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="15a09-323">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn how Copy Activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="15a09-323">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn how Copy Activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="15a09-324">Azure SQL Database data type</span><span class="sxs-lookup"><span data-stu-id="15a09-324">Azure SQL Database data type</span></span> | <span data-ttu-id="15a09-325">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="15a09-325">Data Factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="15a09-326">bigint</span><span class="sxs-lookup"><span data-stu-id="15a09-326">bigint</span></span> |<span data-ttu-id="15a09-327">Int64</span><span class="sxs-lookup"><span data-stu-id="15a09-327">Int64</span></span> |
| <span data-ttu-id="15a09-328">binary</span><span class="sxs-lookup"><span data-stu-id="15a09-328">binary</span></span> |<span data-ttu-id="15a09-329">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-329">Byte[]</span></span> |
| <span data-ttu-id="15a09-330">bit</span><span class="sxs-lookup"><span data-stu-id="15a09-330">bit</span></span> |<span data-ttu-id="15a09-331">Boolean</span><span class="sxs-lookup"><span data-stu-id="15a09-331">Boolean</span></span> |
| <span data-ttu-id="15a09-332">char</span><span class="sxs-lookup"><span data-stu-id="15a09-332">char</span></span> |<span data-ttu-id="15a09-333">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-333">String, Char[]</span></span> |
| <span data-ttu-id="15a09-334">date</span><span class="sxs-lookup"><span data-stu-id="15a09-334">date</span></span> |<span data-ttu-id="15a09-335">DateTime</span><span class="sxs-lookup"><span data-stu-id="15a09-335">DateTime</span></span> |
| <span data-ttu-id="15a09-336">Datetime</span><span class="sxs-lookup"><span data-stu-id="15a09-336">Datetime</span></span> |<span data-ttu-id="15a09-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="15a09-337">DateTime</span></span> |
| <span data-ttu-id="15a09-338">datetime2</span><span class="sxs-lookup"><span data-stu-id="15a09-338">datetime2</span></span> |<span data-ttu-id="15a09-339">DateTime</span><span class="sxs-lookup"><span data-stu-id="15a09-339">DateTime</span></span> |
| <span data-ttu-id="15a09-340">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="15a09-340">Datetimeoffset</span></span> |<span data-ttu-id="15a09-341">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="15a09-341">DateTimeOffset</span></span> |
| <span data-ttu-id="15a09-342">Decimal</span><span class="sxs-lookup"><span data-stu-id="15a09-342">Decimal</span></span> |<span data-ttu-id="15a09-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="15a09-343">Decimal</span></span> |
| <span data-ttu-id="15a09-344">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="15a09-344">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="15a09-345">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-345">Byte[]</span></span> |
| <span data-ttu-id="15a09-346">Float</span><span class="sxs-lookup"><span data-stu-id="15a09-346">Float</span></span> |<span data-ttu-id="15a09-347">Double</span><span class="sxs-lookup"><span data-stu-id="15a09-347">Double</span></span> |
| <span data-ttu-id="15a09-348">image</span><span class="sxs-lookup"><span data-stu-id="15a09-348">image</span></span> |<span data-ttu-id="15a09-349">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-349">Byte[]</span></span> |
| <span data-ttu-id="15a09-350">int</span><span class="sxs-lookup"><span data-stu-id="15a09-350">int</span></span> |<span data-ttu-id="15a09-351">Int32</span><span class="sxs-lookup"><span data-stu-id="15a09-351">Int32</span></span> |
| <span data-ttu-id="15a09-352">money</span><span class="sxs-lookup"><span data-stu-id="15a09-352">money</span></span> |<span data-ttu-id="15a09-353">Decimal</span><span class="sxs-lookup"><span data-stu-id="15a09-353">Decimal</span></span> |
| <span data-ttu-id="15a09-354">nchar</span><span class="sxs-lookup"><span data-stu-id="15a09-354">nchar</span></span> |<span data-ttu-id="15a09-355">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-355">String, Char[]</span></span> |
| <span data-ttu-id="15a09-356">ntext</span><span class="sxs-lookup"><span data-stu-id="15a09-356">ntext</span></span> |<span data-ttu-id="15a09-357">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-357">String, Char[]</span></span> |
| <span data-ttu-id="15a09-358">numeric</span><span class="sxs-lookup"><span data-stu-id="15a09-358">numeric</span></span> |<span data-ttu-id="15a09-359">Decimal</span><span class="sxs-lookup"><span data-stu-id="15a09-359">Decimal</span></span> |
| <span data-ttu-id="15a09-360">nvarchar</span><span class="sxs-lookup"><span data-stu-id="15a09-360">nvarchar</span></span> |<span data-ttu-id="15a09-361">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-361">String, Char[]</span></span> |
| <span data-ttu-id="15a09-362">real</span><span class="sxs-lookup"><span data-stu-id="15a09-362">real</span></span> |<span data-ttu-id="15a09-363">Single</span><span class="sxs-lookup"><span data-stu-id="15a09-363">Single</span></span> |
| <span data-ttu-id="15a09-364">rowversion</span><span class="sxs-lookup"><span data-stu-id="15a09-364">rowversion</span></span> |<span data-ttu-id="15a09-365">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-365">Byte[]</span></span> |
| <span data-ttu-id="15a09-366">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="15a09-366">smalldatetime</span></span> |<span data-ttu-id="15a09-367">DateTime</span><span class="sxs-lookup"><span data-stu-id="15a09-367">DateTime</span></span> |
| <span data-ttu-id="15a09-368">smallint</span><span class="sxs-lookup"><span data-stu-id="15a09-368">smallint</span></span> |<span data-ttu-id="15a09-369">Int16</span><span class="sxs-lookup"><span data-stu-id="15a09-369">Int16</span></span> |
| <span data-ttu-id="15a09-370">smallmoney</span><span class="sxs-lookup"><span data-stu-id="15a09-370">smallmoney</span></span> |<span data-ttu-id="15a09-371">Decimal</span><span class="sxs-lookup"><span data-stu-id="15a09-371">Decimal</span></span> |
| <span data-ttu-id="15a09-372">sql_variant</span><span class="sxs-lookup"><span data-stu-id="15a09-372">sql_variant</span></span> |<span data-ttu-id="15a09-373">Object \*</span><span class="sxs-lookup"><span data-stu-id="15a09-373">Object \*</span></span> |
| <span data-ttu-id="15a09-374">text</span><span class="sxs-lookup"><span data-stu-id="15a09-374">text</span></span> |<span data-ttu-id="15a09-375">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-375">String, Char[]</span></span> |
| <span data-ttu-id="15a09-376">time</span><span class="sxs-lookup"><span data-stu-id="15a09-376">time</span></span> |<span data-ttu-id="15a09-377">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="15a09-377">TimeSpan</span></span> |
| <span data-ttu-id="15a09-378">timestamp</span><span class="sxs-lookup"><span data-stu-id="15a09-378">timestamp</span></span> |<span data-ttu-id="15a09-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-379">Byte[]</span></span> |
| <span data-ttu-id="15a09-380">tinyint</span><span class="sxs-lookup"><span data-stu-id="15a09-380">tinyint</span></span> |<span data-ttu-id="15a09-381">Byte</span><span class="sxs-lookup"><span data-stu-id="15a09-381">Byte</span></span> |
| <span data-ttu-id="15a09-382">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="15a09-382">uniqueidentifier</span></span> |<span data-ttu-id="15a09-383">Guid</span><span class="sxs-lookup"><span data-stu-id="15a09-383">Guid</span></span> |
| <span data-ttu-id="15a09-384">varbinary</span><span class="sxs-lookup"><span data-stu-id="15a09-384">varbinary</span></span> |<span data-ttu-id="15a09-385">Byte[]</span><span class="sxs-lookup"><span data-stu-id="15a09-385">Byte[]</span></span> |
| <span data-ttu-id="15a09-386">varchar</span><span class="sxs-lookup"><span data-stu-id="15a09-386">varchar</span></span> |<span data-ttu-id="15a09-387">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="15a09-387">String, Char[]</span></span> |
| <span data-ttu-id="15a09-388">xml</span><span class="sxs-lookup"><span data-stu-id="15a09-388">xml</span></span> |<span data-ttu-id="15a09-389">Xml</span><span class="sxs-lookup"><span data-stu-id="15a09-389">Xml</span></span> |

## <a name="next-steps"></a><span data-ttu-id="15a09-390">Next steps</span><span class="sxs-lookup"><span data-stu-id="15a09-390">Next steps</span></span>
<span data-ttu-id="15a09-391">For a list of data stores supported as sources and sinks by Copy Activity in Azure Data Factory, see [Supported data stores and formats](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="15a09-391">For a list of data stores supported as sources and sinks by Copy Activity in Azure Data Factory, see [Supported data stores and formats](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
