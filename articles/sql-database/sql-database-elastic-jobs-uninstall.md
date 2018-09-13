---
title: How to uninstall elastic database jobs tool
description: How to uninstall the elastic database jobs tool
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: multiple databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f314ef71e4e799274d599c057b0fdd6baefafc21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553961"
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="40e15-103">Uninstall Elastic Database jobs components</span><span class="sxs-lookup"><span data-stu-id="40e15-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="40e15-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40e15-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="40e15-105">Uninstall Elastic Database jobs components using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="40e15-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="40e15-106">Open the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="40e15-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="40e15-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span><span class="sxs-lookup"><span data-stu-id="40e15-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="40e15-108">Click **Browse** and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="40e15-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="40e15-109">Select the resource group named "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="40e15-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="40e15-110">Delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="40e15-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="40e15-111">Uninstall  Elastic Database jobs components using PowerShell</span><span class="sxs-lookup"><span data-stu-id="40e15-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="40e15-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="40e15-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="40e15-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x\*>cd tools</span><span class="sxs-lookup"><span data-stu-id="40e15-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x\*>cd tools</span></span>
2. <span data-ttu-id="40e15-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="40e15-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="40e15-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="40e15-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="40e15-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span><span class="sxs-lookup"><span data-stu-id="40e15-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="40e15-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="40e15-117">Next steps</span></span>
<span data-ttu-id="40e15-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="40e15-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="40e15-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40e15-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


