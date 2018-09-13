---
title: How to uninstall elastic database jobs tool
description: Learn how to uninstall the elastic database jobs components using the Azure portal of PowerShell.
services: sql-database
manager: craigg
author: stevestein
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 06/14/2018
ms.author: sstein
ms.openlocfilehash: 395bbf50373d3a6e3848fba9fd3db0d6989023f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808807"
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="da20c-103">Uninstall Elastic Database jobs components</span><span class="sxs-lookup"><span data-stu-id="da20c-103">Uninstall Elastic Database jobs components</span></span>


[!INCLUDE [elastic-database-jobs-deprecation](../../includes/sql-database-elastic-jobs-deprecate.md)]


<span data-ttu-id="da20c-104">**Elastic Database jobs** components can be uninstalled using either the Azure portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da20c-104">**Elastic Database jobs** components can be uninstalled using either the Azure portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="da20c-105">Uninstall Elastic Database jobs components using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="da20c-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="da20c-106">Open the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="da20c-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="da20c-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span><span class="sxs-lookup"><span data-stu-id="da20c-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="da20c-108">Click **Browse** and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="da20c-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="da20c-109">Select the resource group named "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="da20c-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="da20c-110">Delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="da20c-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="da20c-111">Uninstall  Elastic Database jobs components using PowerShell</span><span class="sxs-lookup"><span data-stu-id="da20c-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="da20c-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="da20c-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="da20c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x\*>cd tools</span><span class="sxs-lookup"><span data-stu-id="da20c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x\*>cd tools</span></span>
2. <span data-ttu-id="da20c-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="da20c-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="da20c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="da20c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="da20c-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span><span class="sxs-lookup"><span data-stu-id="da20c-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="da20c-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="da20c-117">Next steps</span></span>
<span data-ttu-id="da20c-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="da20c-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="da20c-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da20c-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


