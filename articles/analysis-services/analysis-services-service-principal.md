---
title: Automate Azure Analysis Services tasks with service principals  | Microsoft Docs
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 76cadc453a696b8d19788525bfb69cf9cacd353d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864624"
---
# <a name="automation-with-service-principals"></a><span data-ttu-id="f4022-102">Automation with service principals</span><span class="sxs-lookup"><span data-stu-id="f4022-102">Automation with service principals</span></span>

<span data-ttu-id="f4022-103">Service principals are an Azure Active Directory application resource you create within your tenant to perform unattended resource and service level operations.</span><span class="sxs-lookup"><span data-stu-id="f4022-103">Service principals are an Azure Active Directory application resource you create within your tenant to perform unattended resource and service level operations.</span></span> <span data-ttu-id="f4022-104">They're a unique type of *user identity* with an application ID and password or certificate.</span><span class="sxs-lookup"><span data-stu-id="f4022-104">They're a unique type of *user identity* with an application ID and password or certificate.</span></span> <span data-ttu-id="f4022-105">A service principal has only those permissions necessary to perform tasks defined by the roles and permissions for which it's assigned.</span><span class="sxs-lookup"><span data-stu-id="f4022-105">A service principal has only those permissions necessary to perform tasks defined by the roles and permissions for which it's assigned.</span></span> 

<span data-ttu-id="f4022-106">In Analysis Services, service principals are used with Azure Automation, PowerShell unattended mode, custom client applications, and web apps to automate common tasks.</span><span class="sxs-lookup"><span data-stu-id="f4022-106">In Analysis Services, service principals are used with Azure Automation, PowerShell unattended mode, custom client applications, and web apps to automate common tasks.</span></span> <span data-ttu-id="f4022-107">For example, provisioning servers, deploying models, data refresh, scale up/down, and pause/resume can all be automated by using service principals.</span><span class="sxs-lookup"><span data-stu-id="f4022-107">For example, provisioning servers, deploying models, data refresh, scale up/down, and pause/resume can all be automated by using service principals.</span></span> <span data-ttu-id="f4022-108">Permissions are assigned to service principals through role membership, much like regular Azure AD UPN accounts.</span><span class="sxs-lookup"><span data-stu-id="f4022-108">Permissions are assigned to service principals through role membership, much like regular Azure AD UPN accounts.</span></span>

## <a name="create-service-principals"></a><span data-ttu-id="f4022-109">Create service principals</span><span class="sxs-lookup"><span data-stu-id="f4022-109">Create service principals</span></span>
 
<span data-ttu-id="f4022-110">Service principals can be created in the Azure portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4022-110">Service principals can be created in the Azure portal or by using PowerShell.</span></span> <span data-ttu-id="f4022-111">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="f4022-111">To learn more, see:</span></span>

<span data-ttu-id="f4022-112">[Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) </span><span class="sxs-lookup"><span data-stu-id="f4022-112">[Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) </span></span>  
[<span data-ttu-id="f4022-113">Create service principal - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4022-113">Create service principal - PowerShell</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="store-credential-and-certificate-assets-in-azure-automation"></a><span data-ttu-id="f4022-114">Store credential and certificate assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f4022-114">Store credential and certificate assets in Azure Automation</span></span>

<span data-ttu-id="f4022-115">Service principal credentials and certificates can be stored securely in Azure Automation for runbook operations.</span><span class="sxs-lookup"><span data-stu-id="f4022-115">Service principal credentials and certificates can be stored securely in Azure Automation for runbook operations.</span></span> <span data-ttu-id="f4022-116">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="f4022-116">To learn more, see:</span></span>

<span data-ttu-id="f4022-117">[Credential assets in Azure Automation](../automation/automation-credentials.md) </span><span class="sxs-lookup"><span data-stu-id="f4022-117">[Credential assets in Azure Automation](../automation/automation-credentials.md) </span></span>  
[<span data-ttu-id="f4022-118">Certificate assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f4022-118">Certificate assets in Azure Automation</span></span>](../automation/automation-certificates.md)

## <a name="add-service-principals-to-server-admin-role"></a><span data-ttu-id="f4022-119">Add service principals to server admin role</span><span class="sxs-lookup"><span data-stu-id="f4022-119">Add service principals to server admin role</span></span>

<span data-ttu-id="f4022-120">Before you can use a service principal for Analysis Services server management operations, you must add it to the server administrators role.</span><span class="sxs-lookup"><span data-stu-id="f4022-120">Before you can use a service principal for Analysis Services server management operations, you must add it to the server administrators role.</span></span> <span data-ttu-id="f4022-121">To learn more, see [Add a service principal to the server administrator role](analysis-services-addservprinc-admins.md).</span><span class="sxs-lookup"><span data-stu-id="f4022-121">To learn more, see [Add a service principal to the server administrator role](analysis-services-addservprinc-admins.md).</span></span>

## <a name="service-principals-in-connection-strings"></a><span data-ttu-id="f4022-122">Service principals in connection strings</span><span class="sxs-lookup"><span data-stu-id="f4022-122">Service principals in connection strings</span></span>

<span data-ttu-id="f4022-123">Service principal appID and password or certificate can be used in connection strings much the same as a UPN.</span><span class="sxs-lookup"><span data-stu-id="f4022-123">Service principal appID and password or certificate can be used in connection strings much the same as a UPN.</span></span>

### <a name="powershell"></a><span data-ttu-id="f4022-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4022-124">PowerShell</span></span>

<span data-ttu-id="f4022-125">When using a service principal for resource management operations with the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  module, use `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f4022-125">When using a service principal for resource management operations with the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  module, use `Login-AzureRmAccount` cmdlet.</span></span> <span data-ttu-id="f4022-126">When using a service principal for server operations with the [SQLServer](https://www.powershellgallery.com/packages/SqlServer) module, use `Add-AzureAnalysisServicesAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f4022-126">When using a service principal for server operations with the [SQLServer](https://www.powershellgallery.com/packages/SqlServer) module, use `Add-AzureAnalysisServicesAccount` cmdlet.</span></span> 

<span data-ttu-id="f4022-127">In the following example, appID and a password are used to perform a model database refresh operation:</span><span class="sxs-lookup"><span data-stu-id="f4022-127">In the following example, appID and a password are used to perform a model database refresh operation:</span></span>

```PowerShell
Param (

        [Parameter(Mandatory=$true)] [String] $AppId,
        [Parameter(Mandatory=$true)] [String] $PlainPWord,
        [Parameter(Mandatory=$true)] [String] $TenantId
       )
$PWord = ConvertTo-SecureString -String $PlainPWord -AsPlainText -Force

$Credential = New-Object -TypeName "System.Management.Automation.PSCredential" -ArgumentList $AppId, $PWord

Add-AzureAnalysisServicesAccount -Credential $Credential -ServicePrincipal -TenantId $TenantId -RolloutEnvironment "westcentralus.asazure.windows.net"

Invoke-ProcessTable -Server "asazure://westcentralus.asazure.windows.net/myserver" -TableName "MyTable" -Database "MyDb" -RefreshType "Full"
```

### <a name="amo-and-adomd"></a><span data-ttu-id="f4022-128">AMO and ADOMD</span><span class="sxs-lookup"><span data-stu-id="f4022-128">AMO and ADOMD</span></span> 

<span data-ttu-id="f4022-129">When connecting with client applications and web apps, [AMO and ADOMD client libraries](analysis-services-data-providers.md) version 15.0.2 and higher installable packages from NuGet support service principals in connection strings using the following syntax: `app:AppID` and password or `cert:thumbprint`.</span><span class="sxs-lookup"><span data-stu-id="f4022-129">When connecting with client applications and web apps, [AMO and ADOMD client libraries](analysis-services-data-providers.md) version 15.0.2 and higher installable packages from NuGet support service principals in connection strings using the following syntax: `app:AppID` and password or `cert:thumbprint`.</span></span> 

<span data-ttu-id="f4022-130">In the following example, `appID` and a `password` are used to perform a model database refresh operation:</span><span class="sxs-lookup"><span data-stu-id="f4022-130">In the following example, `appID` and a `password` are used to perform a model database refresh operation:</span></span>

```C#
string appId = "xxx";
string authKey = "yyy";
string connString = $"Provider=MSOLAP;Data Source=asazure://westus.asazure.windows.net/<servername>;User ID=app:{appId};Password={authKey};";
Server server = new Server();
server.Connect(connString);
Database db = server.Databases.FindByName("adventureworks");
Table tbl = db.Model.Tables.Find("DimDate");
tbl.RequestRefresh(RefreshType.Full);
db.Model.SaveChanges();
```

## <a name="next-steps"></a><span data-ttu-id="f4022-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4022-131">Next steps</span></span>
<span data-ttu-id="f4022-132">[Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps) </span><span class="sxs-lookup"><span data-stu-id="f4022-132">[Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps) </span></span>  
[<span data-ttu-id="f4022-133">Add a service principal to the server administrator role</span><span class="sxs-lookup"><span data-stu-id="f4022-133">Add a service principal to the server administrator role</span></span>](analysis-services-addservprinc-admins.md)   