---
title: Copy data to and from Azure SQL Data Warehouse by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from supported source stores to Azure SQL Data Warehouse or from SQL Data Warehouse to supported sink stores by using Data Factory.
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
ms.date: 07/28/2018
ms.author: jingwang
ms.openlocfilehash: ef1bd613943543f78d358064f4abefc6fa31b63e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865451"
---
#  <a name="copy-data-to-or-from-azure-sql-data-warehouse-by-using-azure-data-factory"></a><span data-ttu-id="7f954-103">Copy data to or from Azure SQL Data Warehouse by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7f954-103">Copy data to or from Azure SQL Data Warehouse by using Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you're using:"]
> * [Version1 ](v1/data-factory-azure-sql-data-warehouse-connector.md)
> * [Current version](connector-azure-sql-data-warehouse.md)

<span data-ttu-id="7f954-106">This article explains how to use Copy Activity in Azure Data Factory to copy data to or from Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-106">This article explains how to use Copy Activity in Azure Data Factory to copy data to or from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7f954-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="7f954-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of Copy Activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="7f954-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="7f954-108">Supported capabilities</span></span>

<span data-ttu-id="7f954-109">You can copy data from Azure SQL Data Warehouse to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7f954-109">You can copy data from Azure SQL Data Warehouse to any supported sink data store.</span></span> <span data-ttu-id="7f954-110">And you can copy data from any supported source data store to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-110">And you can copy data from any supported source data store to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7f954-111">For a list of data stores that are supported as sources or sinks by Copy Activity, see the [Supported data stores and formats](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="7f954-111">For a list of data stores that are supported as sources or sinks by Copy Activity, see the [Supported data stores and formats](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="7f954-112">Specifically, this Azure SQL Data Warehouse connector supports these functions:</span><span class="sxs-lookup"><span data-stu-id="7f954-112">Specifically, this Azure SQL Data Warehouse connector supports these functions:</span></span>

- <span data-ttu-id="7f954-113">Copy data by using SQL authentication and Azure Active Directory (Azure AD) Application token authentication with a service principal or Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="7f954-113">Copy data by using SQL authentication and Azure Active Directory (Azure AD) Application token authentication with a service principal or Managed Service Identity (MSI).</span></span>
- <span data-ttu-id="7f954-114">As a source, retrieve data by using a SQL query or stored procedure.</span><span class="sxs-lookup"><span data-stu-id="7f954-114">As a source, retrieve data by using a SQL query or stored procedure.</span></span>
- <span data-ttu-id="7f954-115">As a sink, load data by using PolyBase or a bulk insert.</span><span class="sxs-lookup"><span data-stu-id="7f954-115">As a sink, load data by using PolyBase or a bulk insert.</span></span> <span data-ttu-id="7f954-116">We recommend PolyBase for better copy performance.</span><span class="sxs-lookup"><span data-stu-id="7f954-116">We recommend PolyBase for better copy performance.</span></span>

> [!IMPORTANT]
> Note that PolyBase supports only SQL authentication but not Azure AD authentication.

> [!IMPORTANT]
> If you copy data by using Azure Data Factory Integration Runtime, configure an [Azure SQL server firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) so that Azure services can access the server.
> If you copy data by using a self-hosted integration runtime, configure the Azure SQL server firewall to allow the appropriate IP range. This range includes the machine's IP that is used to connect to Azure SQL Database.

## <a name="get-started"></a><span data-ttu-id="7f954-121">Get started</span><span class="sxs-lookup"><span data-stu-id="7f954-121">Get started</span></span>

> [!TIP]
> To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse. The [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details. For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](load-azure-sql-data-warehouse.md).

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="7f954-125">The following sections provide details about properties that define Data Factory entities specific to an Azure SQL Data Warehouse connector.</span><span class="sxs-lookup"><span data-stu-id="7f954-125">The following sections provide details about properties that define Data Factory entities specific to an Azure SQL Data Warehouse connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7f954-126">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7f954-126">Linked service properties</span></span>

<span data-ttu-id="7f954-127">The following properties are supported for an Azure SQL Data Warehouse linked service:</span><span class="sxs-lookup"><span data-stu-id="7f954-127">The following properties are supported for an Azure SQL Data Warehouse linked service:</span></span>

| <span data-ttu-id="7f954-128">Property</span><span class="sxs-lookup"><span data-stu-id="7f954-128">Property</span></span> | <span data-ttu-id="7f954-129">Description</span><span class="sxs-lookup"><span data-stu-id="7f954-129">Description</span></span> | <span data-ttu-id="7f954-130">Required</span><span class="sxs-lookup"><span data-stu-id="7f954-130">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f954-131">type</span><span class="sxs-lookup"><span data-stu-id="7f954-131">type</span></span> | <span data-ttu-id="7f954-132">The type property must be set to **AzureSqlDW**.</span><span class="sxs-lookup"><span data-stu-id="7f954-132">The type property must be set to **AzureSqlDW**.</span></span> | <span data-ttu-id="7f954-133">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-133">Yes</span></span> |
| <span data-ttu-id="7f954-134">connectionString</span><span class="sxs-lookup"><span data-stu-id="7f954-134">connectionString</span></span> | <span data-ttu-id="7f954-135">Specify the information needed to connect to the Azure SQL Data Warehouse instance for the **connectionString** property.</span><span class="sxs-lookup"><span data-stu-id="7f954-135">Specify the information needed to connect to the Azure SQL Data Warehouse instance for the **connectionString** property.</span></span> <span data-ttu-id="7f954-136">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7f954-136">Mark this field as a **SecureString** to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="7f954-137">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-137">Yes</span></span> |
| <span data-ttu-id="7f954-138">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="7f954-138">servicePrincipalId</span></span> | <span data-ttu-id="7f954-139">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="7f954-139">Specify the application's client ID.</span></span> | <span data-ttu-id="7f954-140">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="7f954-140">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="7f954-141">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="7f954-141">servicePrincipalKey</span></span> | <span data-ttu-id="7f954-142">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="7f954-142">Specify the application's key.</span></span> <span data-ttu-id="7f954-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7f954-143">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="7f954-144">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="7f954-144">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="7f954-145">tenant</span><span class="sxs-lookup"><span data-stu-id="7f954-145">tenant</span></span> | <span data-ttu-id="7f954-146">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="7f954-146">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="7f954-147">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f954-147">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="7f954-148">Yes, when you use Azure AD authentication with a service principal.</span><span class="sxs-lookup"><span data-stu-id="7f954-148">Yes, when you use Azure AD authentication with a service principal.</span></span> |
| <span data-ttu-id="7f954-149">connectVia</span><span class="sxs-lookup"><span data-stu-id="7f954-149">connectVia</span></span> | <span data-ttu-id="7f954-150">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="7f954-150">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="7f954-151">You can use Azure Integration Runtime or a self-hosted integration runtime (if your data store is located in a private network).</span><span class="sxs-lookup"><span data-stu-id="7f954-151">You can use Azure Integration Runtime or a self-hosted integration runtime (if your data store is located in a private network).</span></span> <span data-ttu-id="7f954-152">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="7f954-152">If not specified, it uses the default Azure Integration Runtime.</span></span> | <span data-ttu-id="7f954-153">No</span><span class="sxs-lookup"><span data-stu-id="7f954-153">No</span></span> |

<span data-ttu-id="7f954-154">For different authentication types, refer to the following sections on prerequisites and JSON samples, respectively:</span><span class="sxs-lookup"><span data-stu-id="7f954-154">For different authentication types, refer to the following sections on prerequisites and JSON samples, respectively:</span></span>

- [<span data-ttu-id="7f954-155">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-155">SQL authentication</span></span>](#sql-authentication)
- <span data-ttu-id="7f954-156">Azure AD application token authentication: [Service principal](#service-principal-authentication)</span><span class="sxs-lookup"><span data-stu-id="7f954-156">Azure AD application token authentication: [Service principal](#service-principal-authentication)</span></span>
- <span data-ttu-id="7f954-157">Azure AD application token authentication: [Managed Service Identity](#managed-service-identity-authentication)</span><span class="sxs-lookup"><span data-stu-id="7f954-157">Azure AD application token authentication: [Managed Service Identity](#managed-service-identity-authentication)</span></span>

>[!TIP]
>If you hit error with error code as "UserErrorFailedToConnectToSqlServer" and message like "The session limit for the database is XXX and has been reached.", add `Pooling=false` to your connection string and try again.

### <a name="sql-authentication"></a><span data-ttu-id="7f954-159">SQL authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-159">SQL authentication</span></span>

#### <a name="linked-service-example-that-uses-sql-authentication"></a><span data-ttu-id="7f954-160">Linked service example that uses SQL authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-160">Linked service example that uses SQL authentication</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
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

### <a name="service-principal-authentication"></a><span data-ttu-id="7f954-161">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-161">Service principal authentication</span></span>

<span data-ttu-id="7f954-162">To use service principal-based Azure AD application token authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7f954-162">To use service principal-based Azure AD application token authentication, follow these steps:</span></span>

1. <span data-ttu-id="7f954-163">**[Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)** from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f954-163">**[Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)** from the Azure portal.</span></span> <span data-ttu-id="7f954-164">Make note of the application name and the following values that define the linked service:</span><span class="sxs-lookup"><span data-stu-id="7f954-164">Make note of the application name and the following values that define the linked service:</span></span>

    - <span data-ttu-id="7f954-165">Application ID</span><span class="sxs-lookup"><span data-stu-id="7f954-165">Application ID</span></span>
    - <span data-ttu-id="7f954-166">Application key</span><span class="sxs-lookup"><span data-stu-id="7f954-166">Application key</span></span>
    - <span data-ttu-id="7f954-167">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="7f954-167">Tenant ID</span></span>

1. <span data-ttu-id="7f954-168">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="7f954-168">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span></span> <span data-ttu-id="7f954-169">The Azure AD administrator can be an Azure AD user or Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="7f954-169">The Azure AD administrator can be an Azure AD user or Azure AD group.</span></span> <span data-ttu-id="7f954-170">If you grant the group with MSI an admin role, skip steps 3 and 4.</span><span class="sxs-lookup"><span data-stu-id="7f954-170">If you grant the group with MSI an admin role, skip steps 3 and 4.</span></span> <span data-ttu-id="7f954-171">The administrator will have full access to the database.</span><span class="sxs-lookup"><span data-stu-id="7f954-171">The administrator will have full access to the database.</span></span>

1. <span data-ttu-id="7f954-172">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the service principal.</span><span class="sxs-lookup"><span data-stu-id="7f954-172">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the service principal.</span></span> <span data-ttu-id="7f954-173">Connect to the data warehouse from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span><span class="sxs-lookup"><span data-stu-id="7f954-173">Connect to the data warehouse from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span></span> <span data-ttu-id="7f954-174">Run the following T-SQL:</span><span class="sxs-lookup"><span data-stu-id="7f954-174">Run the following T-SQL:</span></span>
    
    ```sql
    CREATE USER [your application name] FROM EXTERNAL PROVIDER;
    ```

1. <span data-ttu-id="7f954-175">**Grant the service principal needed permissions** as you normally do for SQL users or others.</span><span class="sxs-lookup"><span data-stu-id="7f954-175">**Grant the service principal needed permissions** as you normally do for SQL users or others.</span></span> <span data-ttu-id="7f954-176">Run the following code:</span><span class="sxs-lookup"><span data-stu-id="7f954-176">Run the following code:</span></span>

    ```sql
    EXEC sp_addrolemember [role name], [your application name];
    ```

1. <span data-ttu-id="7f954-177">**Configure an Azure SQL Data Warehouse linked service** in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7f954-177">**Configure an Azure SQL Data Warehouse linked service** in Azure Data Factory.</span></span>


#### <a name="linked-service-example-that-uses-service-principal-authentication"></a><span data-ttu-id="7f954-178">Linked service example that uses service principal authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-178">Linked service example that uses service principal authentication</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
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

### <a name="managed-service-identity-authentication"></a><span data-ttu-id="7f954-179">Managed Service Identity authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-179">Managed Service Identity authentication</span></span>

<span data-ttu-id="7f954-180">A data factory can be associated with a [Managed Service Identity](data-factory-service-identity.md) that represents the specific factory.</span><span class="sxs-lookup"><span data-stu-id="7f954-180">A data factory can be associated with a [Managed Service Identity](data-factory-service-identity.md) that represents the specific factory.</span></span> <span data-ttu-id="7f954-181">You can use this service identity for Azure SQL Data Warehouse authentication.</span><span class="sxs-lookup"><span data-stu-id="7f954-181">You can use this service identity for Azure SQL Data Warehouse authentication.</span></span> <span data-ttu-id="7f954-182">The designated factory can access and copy data from or to your data warehouse by using this identity.</span><span class="sxs-lookup"><span data-stu-id="7f954-182">The designated factory can access and copy data from or to your data warehouse by using this identity.</span></span>

> [!IMPORTANT]
> Note that PolyBase isn't currently supported for MSI authentication.

<span data-ttu-id="7f954-184">To use MSI-based Azure AD application token authentication, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7f954-184">To use MSI-based Azure AD application token authentication, follow these steps:</span></span>

1. <span data-ttu-id="7f954-185">**Create a group in Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="7f954-185">**Create a group in Azure AD.**</span></span> <span data-ttu-id="7f954-186">Make the factory MSI a member of the group.</span><span class="sxs-lookup"><span data-stu-id="7f954-186">Make the factory MSI a member of the group.</span></span>

    1. <span data-ttu-id="7f954-187">Find the data factory service identity from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f954-187">Find the data factory service identity from the Azure portal.</span></span> <span data-ttu-id="7f954-188">Go to your data factory's **Properties**.</span><span class="sxs-lookup"><span data-stu-id="7f954-188">Go to your data factory's **Properties**.</span></span> <span data-ttu-id="7f954-189">Copy the SERVICE IDENTITY ID.</span><span class="sxs-lookup"><span data-stu-id="7f954-189">Copy the SERVICE IDENTITY ID.</span></span>

    1. <span data-ttu-id="7f954-190">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span><span class="sxs-lookup"><span data-stu-id="7f954-190">Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span></span> <span data-ttu-id="7f954-191">Sign in by using the `Connect-AzureAD` command.</span><span class="sxs-lookup"><span data-stu-id="7f954-191">Sign in by using the `Connect-AzureAD` command.</span></span> <span data-ttu-id="7f954-192">Run the following commands to create a group and add the data factory MSI as a member.</span><span class="sxs-lookup"><span data-stu-id="7f954-192">Run the following commands to create a group and add the data factory MSI as a member.</span></span>
    ```powershell
    $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
    Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory service identity ID>"
    ```

1. <span data-ttu-id="7f954-193">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span><span class="sxs-lookup"><span data-stu-id="7f954-193">**[Provision an Azure Active Directory administrator](../sql-database/sql-database-aad-authentication-configure.md#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so.</span></span>

1. <span data-ttu-id="7f954-194">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="7f954-194">**[Create contained database users](../sql-database/sql-database-aad-authentication-configure.md#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the Azure AD group.</span></span> <span data-ttu-id="7f954-195">Connect to the data warehouse from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span><span class="sxs-lookup"><span data-stu-id="7f954-195">Connect to the data warehouse from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission.</span></span> <span data-ttu-id="7f954-196">Run the following T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f954-196">Run the following T-SQL.</span></span> 
    
    ```sql
    CREATE USER [your Azure AD group name] FROM EXTERNAL PROVIDER;
    ```

1. <span data-ttu-id="7f954-197">**Grant the Azure AD group needed permissions** as you normally do for SQL users and others.</span><span class="sxs-lookup"><span data-stu-id="7f954-197">**Grant the Azure AD group needed permissions** as you normally do for SQL users and others.</span></span> <span data-ttu-id="7f954-198">For example, run the following code.</span><span class="sxs-lookup"><span data-stu-id="7f954-198">For example, run the following code.</span></span>

    ```sql
    EXEC sp_addrolemember [role name], [your Azure AD group name];
    ```

1. <span data-ttu-id="7f954-199">**Configure an Azure SQL Data Warehouse linked service** in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7f954-199">**Configure an Azure SQL Data Warehouse linked service** in Azure Data Factory.</span></span>

#### <a name="linked-service-example-that-uses-msi-authentication"></a><span data-ttu-id="7f954-200">Linked service example that uses MSI authentication</span><span class="sxs-lookup"><span data-stu-id="7f954-200">Linked service example that uses MSI authentication</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
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

## <a name="dataset-properties"></a><span data-ttu-id="7f954-201">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7f954-201">Dataset properties</span></span>

<span data-ttu-id="7f954-202">For a full list of sections and properties available for defining datasets, see the [Datasets](https://docs.microsoft.com/en-us/azure/data-factory/concepts-datasets-linked-services) article.</span><span class="sxs-lookup"><span data-stu-id="7f954-202">For a full list of sections and properties available for defining datasets, see the [Datasets](https://docs.microsoft.com/en-us/azure/data-factory/concepts-datasets-linked-services) article.</span></span> <span data-ttu-id="7f954-203">This section provides a list of properties supported by the Azure SQL Data Warehouse dataset.</span><span class="sxs-lookup"><span data-stu-id="7f954-203">This section provides a list of properties supported by the Azure SQL Data Warehouse dataset.</span></span>

<span data-ttu-id="7f954-204">To copy data from or to Azure SQL Data Warehouse, set the **type** property of the dataset to **AzureSqlDWTable**.</span><span class="sxs-lookup"><span data-stu-id="7f954-204">To copy data from or to Azure SQL Data Warehouse, set the **type** property of the dataset to **AzureSqlDWTable**.</span></span> <span data-ttu-id="7f954-205">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="7f954-205">The following properties are supported:</span></span>

| <span data-ttu-id="7f954-206">Property</span><span class="sxs-lookup"><span data-stu-id="7f954-206">Property</span></span> | <span data-ttu-id="7f954-207">Description</span><span class="sxs-lookup"><span data-stu-id="7f954-207">Description</span></span> | <span data-ttu-id="7f954-208">Required</span><span class="sxs-lookup"><span data-stu-id="7f954-208">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f954-209">type</span><span class="sxs-lookup"><span data-stu-id="7f954-209">type</span></span> | <span data-ttu-id="7f954-210">The **type** property of the dataset must be set to **AzureSqlDWTable**.</span><span class="sxs-lookup"><span data-stu-id="7f954-210">The **type** property of the dataset must be set to **AzureSqlDWTable**.</span></span> | <span data-ttu-id="7f954-211">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-211">Yes</span></span> |
| <span data-ttu-id="7f954-212">tableName</span><span class="sxs-lookup"><span data-stu-id="7f954-212">tableName</span></span> | <span data-ttu-id="7f954-213">The name of the table or view in the Azure SQL Data Warehouse instance that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="7f954-213">The name of the table or view in the Azure SQL Data Warehouse instance that the linked service refers to.</span></span> | <span data-ttu-id="7f954-214">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-214">Yes</span></span> |

#### <a name="dataset-properties-example"></a><span data-ttu-id="7f954-215">Dataset properties example</span><span class="sxs-lookup"><span data-stu-id="7f954-215">Dataset properties example</span></span>

```json
{
    "name": "AzureSQLDWDataset",
    "properties":
    {
        "type": "AzureSqlDWTable",
        "linkedServiceName": {
            "referenceName": "<Azure SQL Data Warehouse linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="7f954-216">Copy Activity properties</span><span class="sxs-lookup"><span data-stu-id="7f954-216">Copy Activity properties</span></span>

<span data-ttu-id="7f954-217">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="7f954-217">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="7f954-218">This section provides a list of properties supported by the Azure SQL Data Warehouse source and sink.</span><span class="sxs-lookup"><span data-stu-id="7f954-218">This section provides a list of properties supported by the Azure SQL Data Warehouse source and sink.</span></span>

### <a name="azure-sql-data-warehouse-as-the-source"></a><span data-ttu-id="7f954-219">Azure SQL Data Warehouse as the source</span><span class="sxs-lookup"><span data-stu-id="7f954-219">Azure SQL Data Warehouse as the source</span></span>

<span data-ttu-id="7f954-220">To copy data from Azure SQL Data Warehouse, set the **type** property in the Copy Activity source to **SqlDWSource**.</span><span class="sxs-lookup"><span data-stu-id="7f954-220">To copy data from Azure SQL Data Warehouse, set the **type** property in the Copy Activity source to **SqlDWSource**.</span></span> <span data-ttu-id="7f954-221">The following properties are supported in the Copy Activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="7f954-221">The following properties are supported in the Copy Activity **source** section:</span></span>

| <span data-ttu-id="7f954-222">Property</span><span class="sxs-lookup"><span data-stu-id="7f954-222">Property</span></span> | <span data-ttu-id="7f954-223">Description</span><span class="sxs-lookup"><span data-stu-id="7f954-223">Description</span></span> | <span data-ttu-id="7f954-224">Required</span><span class="sxs-lookup"><span data-stu-id="7f954-224">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f954-225">type</span><span class="sxs-lookup"><span data-stu-id="7f954-225">type</span></span> | <span data-ttu-id="7f954-226">The **type** property of the Copy Activity source must be set to **SqlDWSource**.</span><span class="sxs-lookup"><span data-stu-id="7f954-226">The **type** property of the Copy Activity source must be set to **SqlDWSource**.</span></span> | <span data-ttu-id="7f954-227">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-227">Yes</span></span> |
| <span data-ttu-id="7f954-228">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="7f954-228">sqlReaderQuery</span></span> | <span data-ttu-id="7f954-229">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="7f954-229">Use the custom SQL query to read data.</span></span> <span data-ttu-id="7f954-230">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="7f954-230">Example: `select * from MyTable`.</span></span> | <span data-ttu-id="7f954-231">No</span><span class="sxs-lookup"><span data-stu-id="7f954-231">No</span></span> |
| <span data-ttu-id="7f954-232">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="7f954-232">sqlReaderStoredProcedureName</span></span> | <span data-ttu-id="7f954-233">The name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="7f954-233">The name of the stored procedure that reads data from the source table.</span></span> <span data-ttu-id="7f954-234">The last SQL statement must be a SELECT statement in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="7f954-234">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> | <span data-ttu-id="7f954-235">No</span><span class="sxs-lookup"><span data-stu-id="7f954-235">No</span></span> |
| <span data-ttu-id="7f954-236">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="7f954-236">storedProcedureParameters</span></span> | <span data-ttu-id="7f954-237">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="7f954-237">Parameters for the stored procedure.</span></span><br/><span data-ttu-id="7f954-238">Allowed values are name or value pairs.</span><span class="sxs-lookup"><span data-stu-id="7f954-238">Allowed values are name or value pairs.</span></span> <span data-ttu-id="7f954-239">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="7f954-239">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> | <span data-ttu-id="7f954-240">No</span><span class="sxs-lookup"><span data-stu-id="7f954-240">No</span></span> |

### <a name="points-to-note"></a><span data-ttu-id="7f954-241">Points to note</span><span class="sxs-lookup"><span data-stu-id="7f954-241">Points to note</span></span>

- <span data-ttu-id="7f954-242">If the **sqlReaderQuery** is specified for the **SqlSource**, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span><span class="sxs-lookup"><span data-stu-id="7f954-242">If the **sqlReaderQuery** is specified for the **SqlSource**, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span> <span data-ttu-id="7f954-243">Or you can specify a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="7f954-243">Or you can specify a stored procedure.</span></span> <span data-ttu-id="7f954-244">Specify the **sqlReaderStoredProcedureName** and **storedProcedureParameters** if the stored procedure takes parameters.</span><span class="sxs-lookup"><span data-stu-id="7f954-244">Specify the **sqlReaderStoredProcedureName** and **storedProcedureParameters** if the stored procedure takes parameters.</span></span>
- <span data-ttu-id="7f954-245">If you don't specify either **sqlReaderQuery** or **sqlReaderStoredProcedureName**, the columns defined in the **structure** section of the dataset JSON are used to construct a query.</span><span class="sxs-lookup"><span data-stu-id="7f954-245">If you don't specify either **sqlReaderQuery** or **sqlReaderStoredProcedureName**, the columns defined in the **structure** section of the dataset JSON are used to construct a query.</span></span> <span data-ttu-id="7f954-246">`select column1, column2 from mytable` runs against Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-246">`select column1, column2 from mytable` runs against Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7f954-247">If the dataset definition doesn't have the **structure**, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="7f954-247">If the dataset definition doesn't have the **structure**, all columns are selected from the table.</span></span>
- <span data-ttu-id="7f954-248">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="7f954-248">When you use **sqlReaderStoredProcedureName**, you still need to specify a dummy **tableName** property in the dataset JSON.</span></span>

#### <a name="sql-query-example"></a><span data-ttu-id="7f954-249">SQL query example</span><span class="sxs-lookup"><span data-stu-id="7f954-249">SQL query example</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL DW input dataset name>",
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
                "type": "SqlDWSource",
                "sqlReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

#### <a name="stored-procedure-example"></a><span data-ttu-id="7f954-250">Stored procedure example</span><span class="sxs-lookup"><span data-stu-id="7f954-250">Stored procedure example</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzureSQLDW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure SQL DW input dataset name>",
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
                "type": "SqlDWSource",
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

### <a name="stored-procedure-definition"></a><span data-ttu-id="7f954-251">Stored procedure definition</span><span class="sxs-lookup"><span data-stu-id="7f954-251">Stored procedure definition</span></span>

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

### <a name="azure-sql-data-warehouse-as-sink"></a> <span data-ttu-id="7f954-252">Azure SQL Data Warehouse as sink</span><span class="sxs-lookup"><span data-stu-id="7f954-252">Azure SQL Data Warehouse as sink</span></span>

<span data-ttu-id="7f954-253">To copy data to Azure SQL Data Warehouse, set the sink type in Copy Activity to **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="7f954-253">To copy data to Azure SQL Data Warehouse, set the sink type in Copy Activity to **SqlDWSink**.</span></span> <span data-ttu-id="7f954-254">The following properties are supported in the Copy Activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="7f954-254">The following properties are supported in the Copy Activity **sink** section:</span></span>

| <span data-ttu-id="7f954-255">Property</span><span class="sxs-lookup"><span data-stu-id="7f954-255">Property</span></span> | <span data-ttu-id="7f954-256">Description</span><span class="sxs-lookup"><span data-stu-id="7f954-256">Description</span></span> | <span data-ttu-id="7f954-257">Required</span><span class="sxs-lookup"><span data-stu-id="7f954-257">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f954-258">type</span><span class="sxs-lookup"><span data-stu-id="7f954-258">type</span></span> | <span data-ttu-id="7f954-259">The **type** property of the Copy Activity sink must be set to **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="7f954-259">The **type** property of the Copy Activity sink must be set to **SqlDWSink**.</span></span> | <span data-ttu-id="7f954-260">Yes</span><span class="sxs-lookup"><span data-stu-id="7f954-260">Yes</span></span> |
| <span data-ttu-id="7f954-261">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="7f954-261">allowPolyBase</span></span> | <span data-ttu-id="7f954-262">Indicates whether to use PolyBase, when applicable, instead of the BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="7f954-262">Indicates whether to use PolyBase, when applicable, instead of the BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="7f954-263">We recommend that you load data into SQL Data Warehouse by using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7f954-263">We recommend that you load data into SQL Data Warehouse by using PolyBase.</span></span> <span data-ttu-id="7f954-264">See the [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span><span class="sxs-lookup"><span data-stu-id="7f954-264">See the [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span><br/><br/><span data-ttu-id="7f954-265">Allowed values are **True** and **False** (default).</span><span class="sxs-lookup"><span data-stu-id="7f954-265">Allowed values are **True** and **False** (default).</span></span>  | <span data-ttu-id="7f954-266">No</span><span class="sxs-lookup"><span data-stu-id="7f954-266">No</span></span> |
| <span data-ttu-id="7f954-267">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="7f954-267">polyBaseSettings</span></span> | <span data-ttu-id="7f954-268">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="7f954-268">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> | <span data-ttu-id="7f954-269">No</span><span class="sxs-lookup"><span data-stu-id="7f954-269">No</span></span> |
| <span data-ttu-id="7f954-270">rejectValue</span><span class="sxs-lookup"><span data-stu-id="7f954-270">rejectValue</span></span> | <span data-ttu-id="7f954-271">Specifies the number or percentage of rows that can be rejected before the query fails.</span><span class="sxs-lookup"><span data-stu-id="7f954-271">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span><br/><br/><span data-ttu-id="7f954-272">Learn more about PolyBase’s reject options in the Arguments section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f954-272">Learn more about PolyBase’s reject options in the Arguments section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx).</span></span> <br/><br/><span data-ttu-id="7f954-273">Allowed values are 0 (default), 1, 2, etc.</span><span class="sxs-lookup"><span data-stu-id="7f954-273">Allowed values are 0 (default), 1, 2, etc.</span></span> |<span data-ttu-id="7f954-274">No</span><span class="sxs-lookup"><span data-stu-id="7f954-274">No</span></span> |
| <span data-ttu-id="7f954-275">rejectType</span><span class="sxs-lookup"><span data-stu-id="7f954-275">rejectType</span></span> | <span data-ttu-id="7f954-276">Specifies whether the **rejectValue** option is a literal value or a percentage.</span><span class="sxs-lookup"><span data-stu-id="7f954-276">Specifies whether the **rejectValue** option is a literal value or a percentage.</span></span><br/><br/><span data-ttu-id="7f954-277">Allowed values are **Value** (default) and **Percentage**.</span><span class="sxs-lookup"><span data-stu-id="7f954-277">Allowed values are **Value** (default) and **Percentage**.</span></span> | <span data-ttu-id="7f954-278">No</span><span class="sxs-lookup"><span data-stu-id="7f954-278">No</span></span> |
| <span data-ttu-id="7f954-279">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="7f954-279">rejectSampleValue</span></span> | <span data-ttu-id="7f954-280">Determines the number of rows to retrieve before PolyBase recalculates the percentage of rejected rows.</span><span class="sxs-lookup"><span data-stu-id="7f954-280">Determines the number of rows to retrieve before PolyBase recalculates the percentage of rejected rows.</span></span><br/><br/><span data-ttu-id="7f954-281">Allowed values are 1, 2, etc.</span><span class="sxs-lookup"><span data-stu-id="7f954-281">Allowed values are 1, 2, etc.</span></span> | <span data-ttu-id="7f954-282">Yes, if the **rejectType** is **percentage**.</span><span class="sxs-lookup"><span data-stu-id="7f954-282">Yes, if the **rejectType** is **percentage**.</span></span> |
| <span data-ttu-id="7f954-283">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="7f954-283">useTypeDefault</span></span> | <span data-ttu-id="7f954-284">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span><span class="sxs-lookup"><span data-stu-id="7f954-284">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="7f954-285">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f954-285">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span><br/><br/><span data-ttu-id="7f954-286">Allowed values are **True** and **False** (default).</span><span class="sxs-lookup"><span data-stu-id="7f954-286">Allowed values are **True** and **False** (default).</span></span> | <span data-ttu-id="7f954-287">No</span><span class="sxs-lookup"><span data-stu-id="7f954-287">No</span></span> |
| <span data-ttu-id="7f954-288">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="7f954-288">writeBatchSize</span></span> | <span data-ttu-id="7f954-289">Inserts data into the SQL table when the buffer size reaches **writeBatchSize**.</span><span class="sxs-lookup"><span data-stu-id="7f954-289">Inserts data into the SQL table when the buffer size reaches **writeBatchSize**.</span></span> <span data-ttu-id="7f954-290">Applies only when PolyBase isn't used.</span><span class="sxs-lookup"><span data-stu-id="7f954-290">Applies only when PolyBase isn't used.</span></span><br/><br/><span data-ttu-id="7f954-291">The allowed value is **integer** (number of rows).</span><span class="sxs-lookup"><span data-stu-id="7f954-291">The allowed value is **integer** (number of rows).</span></span> | <span data-ttu-id="7f954-292">No.</span><span class="sxs-lookup"><span data-stu-id="7f954-292">No.</span></span> <span data-ttu-id="7f954-293">The default is 10000.</span><span class="sxs-lookup"><span data-stu-id="7f954-293">The default is 10000.</span></span> |
| <span data-ttu-id="7f954-294">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="7f954-294">writeBatchTimeout</span></span> | <span data-ttu-id="7f954-295">Wait time for the batch insert operation to finish before it times out. Applies only when PolyBase isn't used.</span><span class="sxs-lookup"><span data-stu-id="7f954-295">Wait time for the batch insert operation to finish before it times out. Applies only when PolyBase isn't used.</span></span><br/><br/><span data-ttu-id="7f954-296">The allowed value is **timespan**.</span><span class="sxs-lookup"><span data-stu-id="7f954-296">The allowed value is **timespan**.</span></span> <span data-ttu-id="7f954-297">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="7f954-297">Example: “00:30:00” (30 minutes).</span></span> | <span data-ttu-id="7f954-298">No</span><span class="sxs-lookup"><span data-stu-id="7f954-298">No</span></span> |
| <span data-ttu-id="7f954-299">preCopyScript</span><span class="sxs-lookup"><span data-stu-id="7f954-299">preCopyScript</span></span> | <span data-ttu-id="7f954-300">Specify a SQL query for Copy Activity to run before writing data into Azure SQL Data Warehouse in each run.</span><span class="sxs-lookup"><span data-stu-id="7f954-300">Specify a SQL query for Copy Activity to run before writing data into Azure SQL Data Warehouse in each run.</span></span> <span data-ttu-id="7f954-301">Use this property to clean up the preloaded data.</span><span class="sxs-lookup"><span data-stu-id="7f954-301">Use this property to clean up the preloaded data.</span></span> | <span data-ttu-id="7f954-302">No</span><span class="sxs-lookup"><span data-stu-id="7f954-302">No</span></span> | <span data-ttu-id="7f954-303">(#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="7f954-303">(#repeatability-during-copy).</span></span> | <span data-ttu-id="7f954-304">A query statement.</span><span class="sxs-lookup"><span data-stu-id="7f954-304">A query statement.</span></span> | <span data-ttu-id="7f954-305">No</span><span class="sxs-lookup"><span data-stu-id="7f954-305">No</span></span> |

#### <a name="sql-data-warehouse-sink-example"></a><span data-ttu-id="7f954-306">SQL Data Warehouse sink example</span><span class="sxs-lookup"><span data-stu-id="7f954-306">SQL Data Warehouse sink example</span></span>

```json
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

<span data-ttu-id="7f954-307">Learn more about how to use PolyBase to efficiently load SQL Data Warehouse in the next section.</span><span class="sxs-lookup"><span data-stu-id="7f954-307">Learn more about how to use PolyBase to efficiently load SQL Data Warehouse in the next section.</span></span>

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="7f954-308">Use PolyBase to load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7f954-308">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>

<span data-ttu-id="7f954-309">Using [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) is an efficient way to load a large amount of data into Azure SQL Data Warehouse with high throughput.</span><span class="sxs-lookup"><span data-stu-id="7f954-309">Using [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) is an efficient way to load a large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="7f954-310">You'll see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="7f954-310">You'll see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="7f954-311">See [Performance reference](copy-activity-performance.md#performance-reference) for a detailed comparison.</span><span class="sxs-lookup"><span data-stu-id="7f954-311">See [Performance reference](copy-activity-performance.md#performance-reference) for a detailed comparison.</span></span> <span data-ttu-id="7f954-312">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/data-factory/v1/data-factory-load-sql-data-warehouse).</span><span class="sxs-lookup"><span data-stu-id="7f954-312">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/data-factory/v1/data-factory-load-sql-data-warehouse).</span></span>

* <span data-ttu-id="7f954-313">If your source data is in Azure Blob storage or Azure Data Lake Store, and the format is compatible with PolyBase, copy direct to Azure SQL Data Warehouse by using PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7f954-313">If your source data is in Azure Blob storage or Azure Data Lake Store, and the format is compatible with PolyBase, copy direct to Azure SQL Data Warehouse by using PolyBase.</span></span> <span data-ttu-id="7f954-314">For details, see **[Direct copy by using PolyBase](#direct-copy-by-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="7f954-314">For details, see **[Direct copy by using PolyBase](#direct-copy-by-using-polybase)**.</span></span>
* <span data-ttu-id="7f954-315">If your source data store and format isn't originally supported by PolyBase, use the **[Staged copy by using PolyBase](#staged-copy-by-using-polybase)** feature instead.</span><span class="sxs-lookup"><span data-stu-id="7f954-315">If your source data store and format isn't originally supported by PolyBase, use the **[Staged copy by using PolyBase](#staged-copy-by-using-polybase)** feature instead.</span></span> <span data-ttu-id="7f954-316">The staged copy feature also provides you better throughput.</span><span class="sxs-lookup"><span data-stu-id="7f954-316">The staged copy feature also provides you better throughput.</span></span> <span data-ttu-id="7f954-317">It automatically converts the data into PolyBase-compatible format.</span><span class="sxs-lookup"><span data-stu-id="7f954-317">It automatically converts the data into PolyBase-compatible format.</span></span> <span data-ttu-id="7f954-318">And it stores the data in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f954-318">And it stores the data in Azure Blob storage.</span></span> <span data-ttu-id="7f954-319">It then loads the data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-319">It then loads the data into SQL Data Warehouse.</span></span>

> [!IMPORTANT]
> Note that PolyBase isn't currently supported for MSI-based Azure AD Application token authentication.

### <a name="direct-copy-by-using-polybase"></a><span data-ttu-id="7f954-321">Direct copy by using PolyBase</span><span class="sxs-lookup"><span data-stu-id="7f954-321">Direct copy by using PolyBase</span></span>

<span data-ttu-id="7f954-322">SQL Data Warehouse PolyBase directly supports Azure Blob and Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7f954-322">SQL Data Warehouse PolyBase directly supports Azure Blob and Azure Data Lake Store.</span></span> <span data-ttu-id="7f954-323">It uses service principal as a source and has specific file format requirements.</span><span class="sxs-lookup"><span data-stu-id="7f954-323">It uses service principal as a source and has specific file format requirements.</span></span> <span data-ttu-id="7f954-324">If your source data meets the criteria described in this section, use PolyBase to copy direct from the source data store to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-324">If your source data meets the criteria described in this section, use PolyBase to copy direct from the source data store to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7f954-325">Otherwise, use [Staged copy by using PolyBase](#staged-copy-by-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="7f954-325">Otherwise, use [Staged copy by using PolyBase](#staged-copy-by-using-polybase).</span></span>

> [!TIP]
> To copy data efficiently from Data Lake Store to SQL Data Warehouse, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

<span data-ttu-id="7f954-327">If the requirements aren't met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span><span class="sxs-lookup"><span data-stu-id="7f954-327">If the requirements aren't met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="7f954-328">The **Source linked service** type is Azure Blob storage (**AzureBLobStorage**/**AzureStorage**) with account key authentication or Azure Data Lake Storage Gen1 (**AzureDataLakeStore**) with service principal authentication.</span><span class="sxs-lookup"><span data-stu-id="7f954-328">The **Source linked service** type is Azure Blob storage (**AzureBLobStorage**/**AzureStorage**) with account key authentication or Azure Data Lake Storage Gen1 (**AzureDataLakeStore**) with service principal authentication.</span></span>
2. <span data-ttu-id="7f954-329">The **input dataset** type is **AzureBlob** or **AzureDataLakeStoreFile**.</span><span class="sxs-lookup"><span data-stu-id="7f954-329">The **input dataset** type is **AzureBlob** or **AzureDataLakeStoreFile**.</span></span> <span data-ttu-id="7f954-330">The format type under `type` properties is **OrcFormat**, **ParquetFormat**, or **TextFormat**, with the following configurations:</span><span class="sxs-lookup"><span data-stu-id="7f954-330">The format type under `type` properties is **OrcFormat**, **ParquetFormat**, or **TextFormat**, with the following configurations:</span></span>

   1. <span data-ttu-id="7f954-331">`fileName` doesn't contain wildcard filter.</span><span class="sxs-lookup"><span data-stu-id="7f954-331">`fileName` doesn't contain wildcard filter.</span></span>
   2. <span data-ttu-id="7f954-332">`rowDelimiter` must be **\n**.</span><span class="sxs-lookup"><span data-stu-id="7f954-332">`rowDelimiter` must be **\n**.</span></span>
   3. <span data-ttu-id="7f954-333">`nullValue` is either set to **empty string** ("") or left as default, and `treatEmptyAsNull` is not set to false.</span><span class="sxs-lookup"><span data-stu-id="7f954-333">`nullValue` is either set to **empty string** ("") or left as default, and `treatEmptyAsNull` is not set to false.</span></span>
   4. <span data-ttu-id="7f954-334">`encodingName` is set to **utf-8**, which is the default value.</span><span class="sxs-lookup"><span data-stu-id="7f954-334">`encodingName` is set to **utf-8**, which is the default value.</span></span>
   5. <span data-ttu-id="7f954-335">`escapeChar`, `quoteChar` and `skipLineCount` aren't specified.</span><span class="sxs-lookup"><span data-stu-id="7f954-335">`escapeChar`, `quoteChar` and `skipLineCount` aren't specified.</span></span> <span data-ttu-id="7f954-336">PolyBase support skip header row which can be configured as `firstRowAsHeader` in ADF.</span><span class="sxs-lookup"><span data-stu-id="7f954-336">PolyBase support skip header row which can be configured as `firstRowAsHeader` in ADF.</span></span>
   6. <span data-ttu-id="7f954-337">`compression` can be **no compression**, **GZip**, or **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="7f954-337">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```json
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",
           "nullValue": "",
           "encodingName": "utf-8",
           "firstRowAsHeader": <any>
       },
       "compression": {
           "type": "GZip",
           "level": "Optimal"
       }
    },
    ```

```json
"activities":[
    {
        "name": "CopyFromAzureBlobToSQLDataWarehouseViaPolyBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "BlobDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "AzureSQLDWDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "SqlDWSink",
                "allowPolyBase": true
            }
        }
    }
]
```

### <a name="staged-copy-by-using-polybase"></a><span data-ttu-id="7f954-338">Staged copy by using PolyBase</span><span class="sxs-lookup"><span data-stu-id="7f954-338">Staged copy by using PolyBase</span></span>

<span data-ttu-id="7f954-339">When your source data doesn’t meet the criteria in the previous section, enable data copying via an interim staging Azure Blob storage instance.</span><span class="sxs-lookup"><span data-stu-id="7f954-339">When your source data doesn’t meet the criteria in the previous section, enable data copying via an interim staging Azure Blob storage instance.</span></span> <span data-ttu-id="7f954-340">It can't be Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="7f954-340">It can't be Azure Premium Storage.</span></span> <span data-ttu-id="7f954-341">In this case, Azure Data Factory automatically runs transformations on the data to meet the data format requirements of PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7f954-341">In this case, Azure Data Factory automatically runs transformations on the data to meet the data format requirements of PolyBase.</span></span> <span data-ttu-id="7f954-342">Then it uses PolyBase to load data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-342">Then it uses PolyBase to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="7f954-343">Finally, it cleans up your temporary data from the blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f954-343">Finally, it cleans up your temporary data from the blob storage.</span></span> <span data-ttu-id="7f954-344">See [Staged copy](copy-activity-performance.md#staged-copy) for details about copying data via a staging Azure Blob storage instance.</span><span class="sxs-lookup"><span data-stu-id="7f954-344">See [Staged copy](copy-activity-performance.md#staged-copy) for details about copying data via a staging Azure Blob storage instance.</span></span>

<span data-ttu-id="7f954-345">To use this feature, create an [Azure Storage linked service](connector-azure-blob-storage.md#linked-service-properties) that refers to the Azure storage account with the interim blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f954-345">To use this feature, create an [Azure Storage linked service](connector-azure-blob-storage.md#linked-service-properties) that refers to the Azure storage account with the interim blob storage.</span></span> <span data-ttu-id="7f954-346">Then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="7f954-346">Then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[
    {
        "name": "CopyFromSQLServerToSQLDataWarehouseViaPolyBase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "SQLServerDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "AzureSQLDWDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SqlSource",
            },
            "sink": {
                "type": "SqlDWSink",
                "allowPolyBase": true
            },
            "enableStaging": true,
            "stagingSettings": {
                "linkedServiceName": {
                    "referenceName": "MyStagingBlob",
                    "type": "LinkedServiceReference"
                }
            }
        }
    }
]
```

## <a name="best-practices-for-using-polybase"></a><span data-ttu-id="7f954-347">Best practices for using PolyBase</span><span class="sxs-lookup"><span data-stu-id="7f954-347">Best practices for using PolyBase</span></span>

<span data-ttu-id="7f954-348">The following sections provide best practices in addition to those mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7f954-348">The following sections provide best practices in addition to those mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="7f954-349">Required database permission</span><span class="sxs-lookup"><span data-stu-id="7f954-349">Required database permission</span></span>

<span data-ttu-id="7f954-350">To use PolyBase, the user that loads data into SQL Data Warehouse must have ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span><span class="sxs-lookup"><span data-stu-id="7f954-350">To use PolyBase, the user that loads data into SQL Data Warehouse must have ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="7f954-351">One way to achieve that is to add the user as a member of the **db_owner** role.</span><span class="sxs-lookup"><span data-stu-id="7f954-351">One way to achieve that is to add the user as a member of the **db_owner** role.</span></span> <span data-ttu-id="7f954-352">Learn how to do that in the [SQL Data Warehouse overview](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="7f954-352">Learn how to do that in the [SQL Data Warehouse overview](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limits"></a><span data-ttu-id="7f954-353">Row size and data type limits</span><span class="sxs-lookup"><span data-stu-id="7f954-353">Row size and data type limits</span></span>

<span data-ttu-id="7f954-354">PolyBase loads are limited to rows smaller than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7f954-354">PolyBase loads are limited to rows smaller than 1 MB.</span></span> <span data-ttu-id="7f954-355">They can't load to VARCHR(MAX), NVARCHAR(MAX), or VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="7f954-355">They can't load to VARCHR(MAX), NVARCHAR(MAX), or VARBINARY(MAX).</span></span> <span data-ttu-id="7f954-356">For more information, see [SQL Data Warehouse service capacity limits](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="7f954-356">For more information, see [SQL Data Warehouse service capacity limits](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="7f954-357">When your source data has rows greater than 1 MB, you might want to vertically split the source tables into several small ones.</span><span class="sxs-lookup"><span data-stu-id="7f954-357">When your source data has rows greater than 1 MB, you might want to vertically split the source tables into several small ones.</span></span> <span data-ttu-id="7f954-358">Make sure that the largest size of each row doesn't exceed the limit.</span><span class="sxs-lookup"><span data-stu-id="7f954-358">Make sure that the largest size of each row doesn't exceed the limit.</span></span> <span data-ttu-id="7f954-359">The smaller tables can then be loaded by using PolyBase and merged together in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-359">The smaller tables can then be loaded by using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="7f954-360">SQL Data Warehouse resource class</span><span class="sxs-lookup"><span data-stu-id="7f954-360">SQL Data Warehouse resource class</span></span>

<span data-ttu-id="7f954-361">To achieve the best possible throughput, assign a larger resource class to the user that loads data into SQL Data Warehouse via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7f954-361">To achieve the best possible throughput, assign a larger resource class to the user that loads data into SQL Data Warehouse via PolyBase.</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="7f954-362">**tableName** in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7f954-362">**tableName** in Azure SQL Data Warehouse</span></span>

<span data-ttu-id="7f954-363">The following table gives examples of how to specify the **tableName** property in the JSON dataset.</span><span class="sxs-lookup"><span data-stu-id="7f954-363">The following table gives examples of how to specify the **tableName** property in the JSON dataset.</span></span> <span data-ttu-id="7f954-364">It shows several combinations of schema and table names.</span><span class="sxs-lookup"><span data-stu-id="7f954-364">It shows several combinations of schema and table names.</span></span>

| <span data-ttu-id="7f954-365">DB Schema</span><span class="sxs-lookup"><span data-stu-id="7f954-365">DB Schema</span></span> | <span data-ttu-id="7f954-366">Table name</span><span class="sxs-lookup"><span data-stu-id="7f954-366">Table name</span></span> | <span data-ttu-id="7f954-367">**tableName** JSON property</span><span class="sxs-lookup"><span data-stu-id="7f954-367">**tableName** JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f954-368">dbo</span><span class="sxs-lookup"><span data-stu-id="7f954-368">dbo</span></span> | <span data-ttu-id="7f954-369">MyTable</span><span class="sxs-lookup"><span data-stu-id="7f954-369">MyTable</span></span> | <span data-ttu-id="7f954-370">MyTable or dbo.MyTable or [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="7f954-370">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="7f954-371">dbo1</span><span class="sxs-lookup"><span data-stu-id="7f954-371">dbo1</span></span> | <span data-ttu-id="7f954-372">MyTable</span><span class="sxs-lookup"><span data-stu-id="7f954-372">MyTable</span></span> | <span data-ttu-id="7f954-373">dbo1.MyTable or [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="7f954-373">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="7f954-374">dbo</span><span class="sxs-lookup"><span data-stu-id="7f954-374">dbo</span></span> | <span data-ttu-id="7f954-375">My.Table</span><span class="sxs-lookup"><span data-stu-id="7f954-375">My.Table</span></span> | <span data-ttu-id="7f954-376">[My.Table] or [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="7f954-376">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="7f954-377">dbo1</span><span class="sxs-lookup"><span data-stu-id="7f954-377">dbo1</span></span> | <span data-ttu-id="7f954-378">My.Table</span><span class="sxs-lookup"><span data-stu-id="7f954-378">My.Table</span></span> | <span data-ttu-id="7f954-379">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="7f954-379">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="7f954-380">If you see the following error, the problem might be the value you specified for the **tableName** property.</span><span class="sxs-lookup"><span data-stu-id="7f954-380">If you see the following error, the problem might be the value you specified for the **tableName** property.</span></span> <span data-ttu-id="7f954-381">See the preceding table for the correct way to specify values for the **tableName** JSON property.</span><span class="sxs-lookup"><span data-stu-id="7f954-381">See the preceding table for the correct way to specify values for the **tableName** JSON property.</span></span>

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="7f954-382">Columns with default values</span><span class="sxs-lookup"><span data-stu-id="7f954-382">Columns with default values</span></span>

<span data-ttu-id="7f954-383">Currently, the PolyBase feature in Data Factory accepts only the same number of columns as in the target table.</span><span class="sxs-lookup"><span data-stu-id="7f954-383">Currently, the PolyBase feature in Data Factory accepts only the same number of columns as in the target table.</span></span> <span data-ttu-id="7f954-384">An example is a table with four columns where one of them is defined with a default value.</span><span class="sxs-lookup"><span data-stu-id="7f954-384">An example is a table with four columns where one of them is defined with a default value.</span></span> <span data-ttu-id="7f954-385">The input data still needs to have four columns.</span><span class="sxs-lookup"><span data-stu-id="7f954-385">The input data still needs to have four columns.</span></span> <span data-ttu-id="7f954-386">A three-column input dataset yields an error similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="7f954-386">A three-column input dataset yields an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```

<span data-ttu-id="7f954-387">The NULL value is a special form of the default value.</span><span class="sxs-lookup"><span data-stu-id="7f954-387">The NULL value is a special form of the default value.</span></span> <span data-ttu-id="7f954-388">If the column is nullable, the input data in the blob for that column might be empty.</span><span class="sxs-lookup"><span data-stu-id="7f954-388">If the column is nullable, the input data in the blob for that column might be empty.</span></span> <span data-ttu-id="7f954-389">But it can't be missing from the input dataset.</span><span class="sxs-lookup"><span data-stu-id="7f954-389">But it can't be missing from the input dataset.</span></span> <span data-ttu-id="7f954-390">PolyBase inserts NULL for missing values in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f954-390">PolyBase inserts NULL for missing values in Azure SQL Data Warehouse.</span></span>

## <a name="data-type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="7f954-391">Data type mapping for Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7f954-391">Data type mapping for Azure SQL Data Warehouse</span></span>

<span data-ttu-id="7f954-392">When you copy data from or to Azure SQL Data Warehouse, the following mappings are used from Azure SQL Data Warehouse data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="7f954-392">When you copy data from or to Azure SQL Data Warehouse, the following mappings are used from Azure SQL Data Warehouse data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="7f954-393">See [schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn how Copy Activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="7f954-393">See [schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn how Copy Activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="7f954-394">Azure SQL Data Warehouse data type</span><span class="sxs-lookup"><span data-stu-id="7f954-394">Azure SQL Data Warehouse data type</span></span> | <span data-ttu-id="7f954-395">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="7f954-395">Data Factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f954-396">bigint</span><span class="sxs-lookup"><span data-stu-id="7f954-396">bigint</span></span> | <span data-ttu-id="7f954-397">Int64</span><span class="sxs-lookup"><span data-stu-id="7f954-397">Int64</span></span> |
| <span data-ttu-id="7f954-398">binary</span><span class="sxs-lookup"><span data-stu-id="7f954-398">binary</span></span> | <span data-ttu-id="7f954-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-399">Byte[]</span></span> |
| <span data-ttu-id="7f954-400">bit</span><span class="sxs-lookup"><span data-stu-id="7f954-400">bit</span></span> | <span data-ttu-id="7f954-401">Boolean</span><span class="sxs-lookup"><span data-stu-id="7f954-401">Boolean</span></span> |
| <span data-ttu-id="7f954-402">char</span><span class="sxs-lookup"><span data-stu-id="7f954-402">char</span></span> | <span data-ttu-id="7f954-403">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-403">String, Char[]</span></span> |
| <span data-ttu-id="7f954-404">date</span><span class="sxs-lookup"><span data-stu-id="7f954-404">date</span></span> | <span data-ttu-id="7f954-405">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f954-405">DateTime</span></span> |
| <span data-ttu-id="7f954-406">Datetime</span><span class="sxs-lookup"><span data-stu-id="7f954-406">Datetime</span></span> | <span data-ttu-id="7f954-407">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f954-407">DateTime</span></span> |
| <span data-ttu-id="7f954-408">datetime2</span><span class="sxs-lookup"><span data-stu-id="7f954-408">datetime2</span></span> | <span data-ttu-id="7f954-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f954-409">DateTime</span></span> |
| <span data-ttu-id="7f954-410">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="7f954-410">Datetimeoffset</span></span> | <span data-ttu-id="7f954-411">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="7f954-411">DateTimeOffset</span></span> |
| <span data-ttu-id="7f954-412">Decimal</span><span class="sxs-lookup"><span data-stu-id="7f954-412">Decimal</span></span> | <span data-ttu-id="7f954-413">Decimal</span><span class="sxs-lookup"><span data-stu-id="7f954-413">Decimal</span></span> |
| <span data-ttu-id="7f954-414">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="7f954-414">FILESTREAM attribute (varbinary(max))</span></span> | <span data-ttu-id="7f954-415">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-415">Byte[]</span></span> |
| <span data-ttu-id="7f954-416">Float</span><span class="sxs-lookup"><span data-stu-id="7f954-416">Float</span></span> | <span data-ttu-id="7f954-417">Double</span><span class="sxs-lookup"><span data-stu-id="7f954-417">Double</span></span> |
| <span data-ttu-id="7f954-418">image</span><span class="sxs-lookup"><span data-stu-id="7f954-418">image</span></span> | <span data-ttu-id="7f954-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-419">Byte[]</span></span> |
| <span data-ttu-id="7f954-420">int</span><span class="sxs-lookup"><span data-stu-id="7f954-420">int</span></span> | <span data-ttu-id="7f954-421">Int32</span><span class="sxs-lookup"><span data-stu-id="7f954-421">Int32</span></span> |
| <span data-ttu-id="7f954-422">money</span><span class="sxs-lookup"><span data-stu-id="7f954-422">money</span></span> | <span data-ttu-id="7f954-423">Decimal</span><span class="sxs-lookup"><span data-stu-id="7f954-423">Decimal</span></span> |
| <span data-ttu-id="7f954-424">nchar</span><span class="sxs-lookup"><span data-stu-id="7f954-424">nchar</span></span> | <span data-ttu-id="7f954-425">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-425">String, Char[]</span></span> |
| <span data-ttu-id="7f954-426">ntext</span><span class="sxs-lookup"><span data-stu-id="7f954-426">ntext</span></span> | <span data-ttu-id="7f954-427">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-427">String, Char[]</span></span> |
| <span data-ttu-id="7f954-428">numeric</span><span class="sxs-lookup"><span data-stu-id="7f954-428">numeric</span></span> | <span data-ttu-id="7f954-429">Decimal</span><span class="sxs-lookup"><span data-stu-id="7f954-429">Decimal</span></span> |
| <span data-ttu-id="7f954-430">nvarchar</span><span class="sxs-lookup"><span data-stu-id="7f954-430">nvarchar</span></span> | <span data-ttu-id="7f954-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-431">String, Char[]</span></span> |
| <span data-ttu-id="7f954-432">real</span><span class="sxs-lookup"><span data-stu-id="7f954-432">real</span></span> | <span data-ttu-id="7f954-433">Single</span><span class="sxs-lookup"><span data-stu-id="7f954-433">Single</span></span> |
| <span data-ttu-id="7f954-434">rowversion</span><span class="sxs-lookup"><span data-stu-id="7f954-434">rowversion</span></span> | <span data-ttu-id="7f954-435">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-435">Byte[]</span></span> |
| <span data-ttu-id="7f954-436">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="7f954-436">smalldatetime</span></span> | <span data-ttu-id="7f954-437">DateTime</span><span class="sxs-lookup"><span data-stu-id="7f954-437">DateTime</span></span> |
| <span data-ttu-id="7f954-438">smallint</span><span class="sxs-lookup"><span data-stu-id="7f954-438">smallint</span></span> | <span data-ttu-id="7f954-439">Int16</span><span class="sxs-lookup"><span data-stu-id="7f954-439">Int16</span></span> |
| <span data-ttu-id="7f954-440">smallmoney</span><span class="sxs-lookup"><span data-stu-id="7f954-440">smallmoney</span></span> | <span data-ttu-id="7f954-441">Decimal</span><span class="sxs-lookup"><span data-stu-id="7f954-441">Decimal</span></span> |
| <span data-ttu-id="7f954-442">sql_variant</span><span class="sxs-lookup"><span data-stu-id="7f954-442">sql_variant</span></span> | <span data-ttu-id="7f954-443">Object \*</span><span class="sxs-lookup"><span data-stu-id="7f954-443">Object \*</span></span> |
| <span data-ttu-id="7f954-444">text</span><span class="sxs-lookup"><span data-stu-id="7f954-444">text</span></span> | <span data-ttu-id="7f954-445">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-445">String, Char[]</span></span> |
| <span data-ttu-id="7f954-446">time</span><span class="sxs-lookup"><span data-stu-id="7f954-446">time</span></span> | <span data-ttu-id="7f954-447">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7f954-447">TimeSpan</span></span> |
| <span data-ttu-id="7f954-448">timestamp</span><span class="sxs-lookup"><span data-stu-id="7f954-448">timestamp</span></span> | <span data-ttu-id="7f954-449">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-449">Byte[]</span></span> |
| <span data-ttu-id="7f954-450">tinyint</span><span class="sxs-lookup"><span data-stu-id="7f954-450">tinyint</span></span> | <span data-ttu-id="7f954-451">Byte</span><span class="sxs-lookup"><span data-stu-id="7f954-451">Byte</span></span> |
| <span data-ttu-id="7f954-452">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="7f954-452">uniqueidentifier</span></span> | <span data-ttu-id="7f954-453">Guid</span><span class="sxs-lookup"><span data-stu-id="7f954-453">Guid</span></span> |
| <span data-ttu-id="7f954-454">varbinary</span><span class="sxs-lookup"><span data-stu-id="7f954-454">varbinary</span></span> | <span data-ttu-id="7f954-455">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7f954-455">Byte[]</span></span> |
| <span data-ttu-id="7f954-456">varchar</span><span class="sxs-lookup"><span data-stu-id="7f954-456">varchar</span></span> | <span data-ttu-id="7f954-457">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7f954-457">String, Char[]</span></span> |
| <span data-ttu-id="7f954-458">xml</span><span class="sxs-lookup"><span data-stu-id="7f954-458">xml</span></span> | <span data-ttu-id="7f954-459">Xml</span><span class="sxs-lookup"><span data-stu-id="7f954-459">Xml</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f954-460">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f954-460">Next steps</span></span>
<span data-ttu-id="7f954-461">For a list of data stores supported as sources and sinks by Copy Activity in Azure Data Factory, see [supported data stores and formats](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7f954-461">For a list of data stores supported as sources and sinks by Copy Activity in Azure Data Factory, see [supported data stores and formats](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
