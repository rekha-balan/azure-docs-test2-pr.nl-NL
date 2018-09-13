---
title: Use a Windows VM system-assigned managed identity  to access Azure SQL
description: A tutorial that walks you through the process of using a Windows VM system-assigned managed identity to access Azure SQL.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: bryanla
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: 5f475f62f7b69978bfff62e89260d71cf7207b07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866640"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-sql"></a><span data-ttu-id="23381-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure SQL</span><span class="sxs-lookup"><span data-stu-id="23381-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure SQL</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="23381-104">This tutorial shows you how to use a system-assigned identity for a Windows virtual machine (VM) to access an Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-104">This tutorial shows you how to use a system-assigned identity for a Windows virtual machine (VM) to access an Azure SQL server.</span></span> <span data-ttu-id="23381-105">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="23381-105">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span></span> <span data-ttu-id="23381-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="23381-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="23381-107">Grant your VM access to an Azure SQL server</span><span class="sxs-lookup"><span data-stu-id="23381-107">Grant your VM access to an Azure SQL server</span></span>
> * <span data-ttu-id="23381-108">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group</span><span class="sxs-lookup"><span data-stu-id="23381-108">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group</span></span>
> * <span data-ttu-id="23381-109">Enable Azure AD authentication for the SQL server</span><span class="sxs-lookup"><span data-stu-id="23381-109">Enable Azure AD authentication for the SQL server</span></span>
> * <span data-ttu-id="23381-110">Create a contained user in the database that represents the Azure AD group</span><span class="sxs-lookup"><span data-stu-id="23381-110">Create a contained user in the database that represents the Azure AD group</span></span>
> * <span data-ttu-id="23381-111">Get an access token using the VM identity and use it to query an Azure SQL server</span><span class="sxs-lookup"><span data-stu-id="23381-111">Get an access token using the VM identity and use it to query an Azure SQL server</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23381-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="23381-112">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="23381-113">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="23381-113">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="23381-114">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="23381-114">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="23381-115">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="23381-115">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-a-database-in-an-azure-sql-server"></a><span data-ttu-id="23381-116">Grant your VM access to a database in an Azure SQL server</span><span class="sxs-lookup"><span data-stu-id="23381-116">Grant your VM access to a database in an Azure SQL server</span></span>

<span data-ttu-id="23381-117">Now you can grant your VM access to a database in an Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-117">Now you can grant your VM access to a database in an Azure SQL server.</span></span>  <span data-ttu-id="23381-118">For this step, you can use an existing SQL server or create a new one.</span><span class="sxs-lookup"><span data-stu-id="23381-118">For this step, you can use an existing SQL server or create a new one.</span></span>  <span data-ttu-id="23381-119">To create a new server and database using the Azure portal, follow this [Azure SQL quickstart](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="23381-119">To create a new server and database using the Azure portal, follow this [Azure SQL quickstart](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span></span> <span data-ttu-id="23381-120">There are also quickstarts that use the Azure CLI and Azure PowerShell in the [Azure SQL documentation](https://docs.microsoft.com/azure/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="23381-120">There are also quickstarts that use the Azure CLI and Azure PowerShell in the [Azure SQL documentation](https://docs.microsoft.com/azure/sql-database/).</span></span>

<span data-ttu-id="23381-121">There are three steps to granting your VM access to a database:</span><span class="sxs-lookup"><span data-stu-id="23381-121">There are three steps to granting your VM access to a database:</span></span>
1.  <span data-ttu-id="23381-122">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group.</span><span class="sxs-lookup"><span data-stu-id="23381-122">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group.</span></span>
2.  <span data-ttu-id="23381-123">Enable Azure AD authentication for the SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-123">Enable Azure AD authentication for the SQL server.</span></span>
3.  <span data-ttu-id="23381-124">Create a **contained user** in the database that represents the Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="23381-124">Create a **contained user** in the database that represents the Azure AD group.</span></span>

> [!NOTE]
> <span data-ttu-id="23381-125">Normally you would create a contained user that maps directly to the VM's system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="23381-125">Normally you would create a contained user that maps directly to the VM's system-assigned managed identity.</span></span>  <span data-ttu-id="23381-126">Currently, Azure SQL does not allow the Azure AD Service Principal that represents the VM's system-assigned managed identity to be mapped to a contained user.</span><span class="sxs-lookup"><span data-stu-id="23381-126">Currently, Azure SQL does not allow the Azure AD Service Principal that represents the VM's system-assigned managed identity to be mapped to a contained user.</span></span>  <span data-ttu-id="23381-127">As a supported workaround, you make the VM's system-assigned managed identity a member of an Azure AD group, then create a contained user in the database that represents the group.</span><span class="sxs-lookup"><span data-stu-id="23381-127">As a supported workaround, you make the VM's system-assigned managed identity a member of an Azure AD group, then create a contained user in the database that represents the group.</span></span>


## <a name="create-a-group-in-azure-ad-and-make-the-vms-system-assigned-managed-identity-a-member-of-the-group"></a><span data-ttu-id="23381-128">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group</span><span class="sxs-lookup"><span data-stu-id="23381-128">Create a group in Azure AD and make the VM's system-assigned managed identity a member of the group</span></span>

<span data-ttu-id="23381-129">You can use an existing Azure AD group, or create a new one using Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23381-129">You can use an existing Azure AD group, or create a new one using Azure AD PowerShell.</span></span>  

<span data-ttu-id="23381-130">First, install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span><span class="sxs-lookup"><span data-stu-id="23381-130">First, install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module.</span></span> <span data-ttu-id="23381-131">Then sign in using `Connect-AzureAD`, and run the following command to create the group, and save it in a variable:</span><span class="sxs-lookup"><span data-stu-id="23381-131">Then sign in using `Connect-AzureAD`, and run the following command to create the group, and save it in a variable:</span></span>

```powershell
$Group = New-AzureADGroup -DisplayName "VM managed identity access to SQL" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
```

<span data-ttu-id="23381-132">The output looks like the following, which also examines the value of the variable:</span><span class="sxs-lookup"><span data-stu-id="23381-132">The output looks like the following, which also examines the value of the variable:</span></span>

```powershell
$Group = New-AzureADGroup -DisplayName "VM managed identity access to SQL" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
$Group
ObjectId                             DisplayName          Description
--------                             -----------          -----------
6de75f3c-8b2f-4bf4-b9f8-78cc60a18050 VM managed identity access to SQL
```

<span data-ttu-id="23381-133">Next, add the VM's system-assigned managed identity to the group.</span><span class="sxs-lookup"><span data-stu-id="23381-133">Next, add the VM's system-assigned managed identity to the group.</span></span>  <span data-ttu-id="23381-134">You need the system-assigned managed identity's **ObjectId**, which you can get using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23381-134">You need the system-assigned managed identity's **ObjectId**, which you can get using Azure PowerShell.</span></span>  <span data-ttu-id="23381-135">First, download [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="23381-135">First, download [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="23381-136">Then sign in using `Connect-AzureRmAccount`, and run the following commands to:</span><span class="sxs-lookup"><span data-stu-id="23381-136">Then sign in using `Connect-AzureRmAccount`, and run the following commands to:</span></span>
- <span data-ttu-id="23381-137">Ensure your session context is set to the desired Azure subscription, if you have multiple ones.</span><span class="sxs-lookup"><span data-stu-id="23381-137">Ensure your session context is set to the desired Azure subscription, if you have multiple ones.</span></span>
- <span data-ttu-id="23381-138">List the available resources in your Azure subscription, in verify the correct resource group and VM names.</span><span class="sxs-lookup"><span data-stu-id="23381-138">List the available resources in your Azure subscription, in verify the correct resource group and VM names.</span></span>
- <span data-ttu-id="23381-139">Get the VM's system-assigned managed identity properties, using the appropriate values for `<RESOURCE-GROUP>` and `<VM-NAME>`.</span><span class="sxs-lookup"><span data-stu-id="23381-139">Get the VM's system-assigned managed identity properties, using the appropriate values for `<RESOURCE-GROUP>` and `<VM-NAME>`.</span></span>

```powershell
Set-AzureRMContext -subscription "bdc79274-6bb9-48a8-bfd8-00c140fxxxx"
Get-AzureRmResource
$VM = Get-AzureRmVm -ResourceGroup <RESOURCE-GROUP> -Name <VM-NAME>
```

<span data-ttu-id="23381-140">The output looks like the following, which also examines the service principal Object ID of the VM's system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="23381-140">The output looks like the following, which also examines the service principal Object ID of the VM's system-assigned managed identity:</span></span>
```powershell
$VM = Get-AzureRmVm -ResourceGroup DevTestGroup -Name DevTestWinVM
$VM.Identity.PrincipalId
b83305de-f496-49ca-9427-e77512f6cc64
```

<span data-ttu-id="23381-141">Now add the VM's system-assigned managed identity to the group.</span><span class="sxs-lookup"><span data-stu-id="23381-141">Now add the VM's system-assigned managed identity to the group.</span></span>  <span data-ttu-id="23381-142">You can only add a service principal to a group using Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23381-142">You can only add a service principal to a group using Azure AD PowerShell.</span></span>  <span data-ttu-id="23381-143">Run this command:</span><span class="sxs-lookup"><span data-stu-id="23381-143">Run this command:</span></span>
```powershell
Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId $VM.Identity.PrincipalId
```

<span data-ttu-id="23381-144">If you also examine the group membership afterward, the output looks as follows:</span><span class="sxs-lookup"><span data-stu-id="23381-144">If you also examine the group membership afterward, the output looks as follows:</span></span>

```powershell
Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId $VM.Identity.PrincipalId
Get-AzureAdGroupMember -ObjectId $Group.ObjectId

ObjectId                             AppId                                DisplayName
--------                             -----                                -----------
b83305de-f496-49ca-9427-e77512f6cc64 0b67a6d6-6090-4ab4-b423-d6edda8e5d9f DevTestWinVM
```

## <a name="enable-azure-ad-authentication-for-the-sql-server"></a><span data-ttu-id="23381-145">Enable Azure AD authentication for the SQL server</span><span class="sxs-lookup"><span data-stu-id="23381-145">Enable Azure AD authentication for the SQL server</span></span>

<span data-ttu-id="23381-146">Now that you have created the group and added the VM's system-assigned managed identity to the membership, you can [configure Azure AD authentication for the SQL server](/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-server) using the following steps:</span><span class="sxs-lookup"><span data-stu-id="23381-146">Now that you have created the group and added the VM's system-assigned managed identity to the membership, you can [configure Azure AD authentication for the SQL server](/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-server) using the following steps:</span></span>

1.  <span data-ttu-id="23381-147">In the Azure portal, select **SQL servers** from the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="23381-147">In the Azure portal, select **SQL servers** from the left-hand navigation.</span></span>
2.  <span data-ttu-id="23381-148">Click the SQL server to be enabled for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="23381-148">Click the SQL server to be enabled for Azure AD authentication.</span></span>
3.  <span data-ttu-id="23381-149">In the **Settings** section of the blade, click **Active Directory admin**.</span><span class="sxs-lookup"><span data-stu-id="23381-149">In the **Settings** section of the blade, click **Active Directory admin**.</span></span>
4.  <span data-ttu-id="23381-150">In the command bar, click **Set admin**.</span><span class="sxs-lookup"><span data-stu-id="23381-150">In the command bar, click **Set admin**.</span></span>
5.  <span data-ttu-id="23381-151">Select an Azure AD user account to be made an administrator of the server, and click **Select.**</span><span class="sxs-lookup"><span data-stu-id="23381-151">Select an Azure AD user account to be made an administrator of the server, and click **Select.**</span></span>
6.  <span data-ttu-id="23381-152">In the command bar, click **Save.**</span><span class="sxs-lookup"><span data-stu-id="23381-152">In the command bar, click **Save.**</span></span>

## <a name="create-a-contained-user-in-the-database-that-represents-the-azure-ad-group"></a><span data-ttu-id="23381-153">Create a contained user in the database that represents the Azure AD group</span><span class="sxs-lookup"><span data-stu-id="23381-153">Create a contained user in the database that represents the Azure AD group</span></span>

<span data-ttu-id="23381-154">For this next step, you will need [Microsoft SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="23381-154">For this next step, you will need [Microsoft SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="23381-155">Before beginning, it may also be helpful to review the following articles for background on Azure AD integration:</span><span class="sxs-lookup"><span data-stu-id="23381-155">Before beginning, it may also be helpful to review the following articles for background on Azure AD integration:</span></span>

- [<span data-ttu-id="23381-156">Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)</span><span class="sxs-lookup"><span data-stu-id="23381-156">Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)</span></span>](/azure/sql-database/sql-database-ssms-mfa-authentication)
- [<span data-ttu-id="23381-157">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="23381-157">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>](/azure/sql-database/sql-database-aad-authentication-configure)

1.  <span data-ttu-id="23381-158">Start SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="23381-158">Start SQL Server Management Studio.</span></span>
2.  <span data-ttu-id="23381-159">In the **Connect to Server** dialog, Enter your SQL server name in the **Server name** field.</span><span class="sxs-lookup"><span data-stu-id="23381-159">In the **Connect to Server** dialog, Enter your SQL server name in the **Server name** field.</span></span>
3.  <span data-ttu-id="23381-160">In the **Authentication** field, select **Active Directory - Universal with MFA support**.</span><span class="sxs-lookup"><span data-stu-id="23381-160">In the **Authentication** field, select **Active Directory - Universal with MFA support**.</span></span>
4.  <span data-ttu-id="23381-161">In the **User name** field, enter the name of the Azure AD account that you set as the server administrator, for example, helen@woodgroveonline.com</span><span class="sxs-lookup"><span data-stu-id="23381-161">In the **User name** field, enter the name of the Azure AD account that you set as the server administrator, for example, helen@woodgroveonline.com</span></span>
5.  <span data-ttu-id="23381-162">Click **Options**.</span><span class="sxs-lookup"><span data-stu-id="23381-162">Click **Options**.</span></span>
6.  <span data-ttu-id="23381-163">In the **Connect to database** field, enter the name of the non-system database you want to configure.</span><span class="sxs-lookup"><span data-stu-id="23381-163">In the **Connect to database** field, enter the name of the non-system database you want to configure.</span></span>
7.  <span data-ttu-id="23381-164">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="23381-164">Click **Connect**.</span></span>  <span data-ttu-id="23381-165">Complete the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="23381-165">Complete the sign-in process.</span></span>
8.  <span data-ttu-id="23381-166">In the **Object Explorer**, expand the **Databases** folder.</span><span class="sxs-lookup"><span data-stu-id="23381-166">In the **Object Explorer**, expand the **Databases** folder.</span></span>
9.  <span data-ttu-id="23381-167">Right-click on a user database and click **New query**.</span><span class="sxs-lookup"><span data-stu-id="23381-167">Right-click on a user database and click **New query**.</span></span>
10.  <span data-ttu-id="23381-168">In the query window, enter the following line, and click **Execute** in the toolbar:</span><span class="sxs-lookup"><span data-stu-id="23381-168">In the query window, enter the following line, and click **Execute** in the toolbar:</span></span>
    
     ```
     CREATE USER [VM managed identity access to SQL] FROM EXTERNAL PROVIDER
     ```
    
     <span data-ttu-id="23381-169">The command should complete successfully, creating the contained user for the group.</span><span class="sxs-lookup"><span data-stu-id="23381-169">The command should complete successfully, creating the contained user for the group.</span></span>
11.  <span data-ttu-id="23381-170">Clear the query window, enter the following line, and click **Execute** in the toolbar:</span><span class="sxs-lookup"><span data-stu-id="23381-170">Clear the query window, enter the following line, and click **Execute** in the toolbar:</span></span>
     
     ```
     ALTER ROLE db_datareader ADD MEMBER [VM VM managed identity access to SQL access to SQL]
     ```

     <span data-ttu-id="23381-171">The command should complete successfully, granting the contained user the ability to read the entire database.</span><span class="sxs-lookup"><span data-stu-id="23381-171">The command should complete successfully, granting the contained user the ability to read the entire database.</span></span>

<span data-ttu-id="23381-172">Code running in the VM can now get a token using its system-assigned managed identity and use the token to authenticate to the SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-172">Code running in the VM can now get a token using its system-assigned managed identity and use the token to authenticate to the SQL server.</span></span>

## <a name="get-an-access-token-using-the-vms-system-assigned-managed-identity-and-use-it-to-call-azure-sql"></a><span data-ttu-id="23381-173">Get an access token using the VM's system-assigned managed identity and use it to call Azure SQL</span><span class="sxs-lookup"><span data-stu-id="23381-173">Get an access token using the VM's system-assigned managed identity and use it to call Azure SQL</span></span> 

<span data-ttu-id="23381-174">Azure SQL natively supports Azure AD authentication, so it can directly accept access tokens obtained using managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="23381-174">Azure SQL natively supports Azure AD authentication, so it can directly accept access tokens obtained using managed identities for Azure resources.</span></span>  <span data-ttu-id="23381-175">You use the **access token** method of creating a connection to SQL.</span><span class="sxs-lookup"><span data-stu-id="23381-175">You use the **access token** method of creating a connection to SQL.</span></span>  <span data-ttu-id="23381-176">This is part of Azure SQL's integration with Azure AD, and is different from supplying credentials on the connection string.</span><span class="sxs-lookup"><span data-stu-id="23381-176">This is part of Azure SQL's integration with Azure AD, and is different from supplying credentials on the connection string.</span></span>

<span data-ttu-id="23381-177">Here's a .Net code example of opening a connection to SQL using an access token.</span><span class="sxs-lookup"><span data-stu-id="23381-177">Here's a .Net code example of opening a connection to SQL using an access token.</span></span>  <span data-ttu-id="23381-178">This code must run on the VM to be able to access the VM's system-assigned managed identity's endpoint.</span><span class="sxs-lookup"><span data-stu-id="23381-178">This code must run on the VM to be able to access the VM's system-assigned managed identity's endpoint.</span></span>  <span data-ttu-id="23381-179">**.Net Framework 4.6** or higher is required to use the access token method.</span><span class="sxs-lookup"><span data-stu-id="23381-179">**.Net Framework 4.6** or higher is required to use the access token method.</span></span>  <span data-ttu-id="23381-180">Replace the values of AZURE-SQL-SERVERNAME and DATABASE accordingly.</span><span class="sxs-lookup"><span data-stu-id="23381-180">Replace the values of AZURE-SQL-SERVERNAME and DATABASE accordingly.</span></span>  <span data-ttu-id="23381-181">Note the resource ID for Azure SQL is "https://database.windows.net/".</span><span class="sxs-lookup"><span data-stu-id="23381-181">Note the resource ID for Azure SQL is "https://database.windows.net/".</span></span>

```csharp
using System.Net;
using System.IO;
using System.Data.SqlClient;
using System.Web.Script.Serialization;

//
// Get an access token for SQL.
//
HttpWebRequest request = (HttpWebRequest)WebRequest.Create("http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://database.windows.net/");
request.Headers["Metadata"] = "true";
request.Method = "GET";
string accessToken = null;

try
{
    // Call managed identities for Azure resources endpoint.
    HttpWebResponse response = (HttpWebResponse)request.GetResponse();

    // Pipe response Stream to a StreamReader and extract access token.
    StreamReader streamResponse = new StreamReader(response.GetResponseStream()); 
    string stringResponse = streamResponse.ReadToEnd();
    JavaScriptSerializer j = new JavaScriptSerializer();
    Dictionary<string, string> list = (Dictionary<string, string>) j.Deserialize(stringResponse, typeof(Dictionary<string, string>));
    accessToken = list["access_token"];
}
catch (Exception e)
{
    string errorText = String.Format("{0} \n\n{1}", e.Message, e.InnerException != null ? e.InnerException.Message : "Acquire token failed");
}

//
// Open a connection to the SQL server using the access token.
//
if (accessToken != null) {
    string connectionString = "Data Source=<AZURE-SQL-SERVERNAME>; Initial Catalog=<DATABASE>;";
    SqlConnection conn = new SqlConnection(connectionString);
    conn.AccessToken = accessToken;
    conn.Open();
}
```

<span data-ttu-id="23381-182">Alternatively, a quick way to test the end to end setup without having to write and deploy an app on the VM is using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23381-182">Alternatively, a quick way to test the end to end setup without having to write and deploy an app on the VM is using PowerShell.</span></span>

1.  <span data-ttu-id="23381-183">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="23381-183">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span></span> 
2.  <span data-ttu-id="23381-184">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="23381-184">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3.  <span data-ttu-id="23381-185">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span><span class="sxs-lookup"><span data-stu-id="23381-185">Now that you have created a **Remote Desktop Connection** with the virtual machine, open **PowerShell** in the remote session.</span></span> 
4.  <span data-ttu-id="23381-186">Using PowerShell’s `Invoke-WebRequest`, make a request to the local managed identity's endpoint to get an access token for Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="23381-186">Using PowerShell’s `Invoke-WebRequest`, make a request to the local managed identity's endpoint to get an access token for Azure SQL.</span></span>

    ```powershell
       $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fdatabase.windows.net%2F' -Method GET -Headers @{Metadata="true"}
    ```
    
    <span data-ttu-id="23381-187">Convert the response from a JSON object to a PowerShell object.</span><span class="sxs-lookup"><span data-stu-id="23381-187">Convert the response from a JSON object to a PowerShell object.</span></span> 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```

    <span data-ttu-id="23381-188">Extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="23381-188">Extract the access token from the response.</span></span>
    
    ```powershell
    $AccessToken = $content.access_token
    ```

5.  <span data-ttu-id="23381-189">Open a connection to the SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-189">Open a connection to the SQL server.</span></span> <span data-ttu-id="23381-190">Remember to replace the values for AZURE-SQL-SERVERNAME and DATABASE.</span><span class="sxs-lookup"><span data-stu-id="23381-190">Remember to replace the values for AZURE-SQL-SERVERNAME and DATABASE.</span></span>
    
    ```powershell
    $SqlConnection = New-Object System.Data.SqlClient.SqlConnection
    $SqlConnection.ConnectionString = "Data Source = <AZURE-SQL-SERVERNAME>; Initial Catalog = <DATABASE>"
    $SqlConnection.AccessToken = $AccessToken
    $SqlConnection.Open()
    ```

    <span data-ttu-id="23381-191">Next, create and send a query to the server.</span><span class="sxs-lookup"><span data-stu-id="23381-191">Next, create and send a query to the server.</span></span>  <span data-ttu-id="23381-192">Remember to replace the value for TABLE.</span><span class="sxs-lookup"><span data-stu-id="23381-192">Remember to replace the value for TABLE.</span></span>

    ```powershell
    $SqlCmd = New-Object System.Data.SqlClient.SqlCommand
    $SqlCmd.CommandText = "SELECT * from <TABLE>;"
    $SqlCmd.Connection = $SqlConnection
    $SqlAdapter = New-Object System.Data.SqlClient.SqlDataAdapter
    $SqlAdapter.SelectCommand = $SqlCmd
    $DataSet = New-Object System.Data.DataSet
    $SqlAdapter.Fill($DataSet)
    ```

<span data-ttu-id="23381-193">Examine the value of `$DataSet.Tables[0]` to view the results of the query.</span><span class="sxs-lookup"><span data-stu-id="23381-193">Examine the value of `$DataSet.Tables[0]` to view the results of the query.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23381-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="23381-194">Next steps</span></span>

<span data-ttu-id="23381-195">In this tutorial, you learned how to use a system-assigned managed identity to access Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="23381-195">In this tutorial, you learned how to use a system-assigned managed identity to access Azure SQL server.</span></span>  <span data-ttu-id="23381-196">To learn more about Azure SQL Server see:</span><span class="sxs-lookup"><span data-stu-id="23381-196">To learn more about Azure SQL Server see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="23381-197">Azure SQL Database service</span><span class="sxs-lookup"><span data-stu-id="23381-197">Azure SQL Database service</span></span>](/azure/sql-database/sql-database-technical-overview)
