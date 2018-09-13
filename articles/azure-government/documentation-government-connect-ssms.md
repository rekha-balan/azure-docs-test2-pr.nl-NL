---
title: Connect to Azure Government with SQL Server Management Studio | Microsoft Docs
description: Manage your subscription in Azure Government by connecting with SSMS.
services: azure-government
cloud: gov
documentationcenter: ''
author: yujhongmicrosoft
manager: zakramer
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 08/10/2018
ms.author: yujhong
ms.openlocfilehash: 3b9647e1d533afe41afed0d6c733a2adb01098d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868118"
---
# <a name="develop-with-sql-server-management-studio"></a><span data-ttu-id="89461-103">Develop with SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="89461-103">Develop with SQL Server Management Studio</span></span> 

<span data-ttu-id="89461-104">To use SQL Server Management Studio (SSMS) with Azure Government, specify Azure Government as the environment to connect to, rather than global Azure.</span><span class="sxs-lookup"><span data-stu-id="89461-104">To use SQL Server Management Studio (SSMS) with Azure Government, specify Azure Government as the environment to connect to, rather than global Azure.</span></span> <span data-ttu-id="89461-105">To connect to computers that are running SQL Server in your Azure Government subscription, you must configure SSMS to connect to the Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="89461-105">To connect to computers that are running SQL Server in your Azure Government subscription, you must configure SSMS to connect to the Azure Government cloud.</span></span> 

<span data-ttu-id="89461-106">For general information about SSMS, see the [SSMS documentation](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="89461-106">For general information about SSMS, see the [SSMS documentation](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

<span data-ttu-id="89461-107">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="89461-107">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89461-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="89461-108">Prerequisites</span></span>

* <span data-ttu-id="89461-109">Review [Guidance for developers](documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="89461-109">Review [Guidance for developers](documentation-government-developer-guide.md).</span></span><br/> <span data-ttu-id="89461-110">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span><span class="sxs-lookup"><span data-stu-id="89461-110">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span></span> <span data-ttu-id="89461-111">You must know about these endpoints in order to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="89461-111">You must know about these endpoints in order to connect to Azure Government.</span></span> 
* <span data-ttu-id="89461-112">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span><span class="sxs-lookup"><span data-stu-id="89461-112">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span></span>

## <a name="set-up-an-azure-sql-server-firewall-rule"></a><span data-ttu-id="89461-113">Set up an Azure SQL Server firewall rule</span><span class="sxs-lookup"><span data-stu-id="89461-113">Set up an Azure SQL Server firewall rule</span></span>

<span data-ttu-id="89461-114">Before you connect to Azure Government from SSMS, you must set up an Azure SQL Server firewall rule to allow your local IP address to access your computer that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89461-114">Before you connect to Azure Government from SSMS, you must set up an Azure SQL Server firewall rule to allow your local IP address to access your computer that's running SQL Server.</span></span> 

<span data-ttu-id="89461-115">Follow these steps to [Manage firewall rules by using the Azure portal](../sql-database/sql-database-firewall-configure.md#manage-firewall-rules-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="89461-115">Follow these steps to [Manage firewall rules by using the Azure portal](../sql-database/sql-database-firewall-configure.md#manage-firewall-rules-using-the-azure-portal).</span></span> 

## <a name="specify-azure-government-as-the-environment-to-connect"></a><span data-ttu-id="89461-116">Specify Azure Government as the environment to connect</span><span class="sxs-lookup"><span data-stu-id="89461-116">Specify Azure Government as the environment to connect</span></span>

1. <span data-ttu-id="89461-117">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="89461-117">Open SSMS.</span></span> <span data-ttu-id="89461-118">Browse to **Tools** > **Options** > **Azure Services**.</span><span class="sxs-lookup"><span data-stu-id="89461-118">Browse to **Tools** > **Options** > **Azure Services**.</span></span>

    ![SSMS Tools](./media/documentation-government-connect-with-ssms-img1.png)

2. <span data-ttu-id="89461-120">In the **Select an Azure Cloud** drop-down, select **AzureUSGovernment**.</span><span class="sxs-lookup"><span data-stu-id="89461-120">In the **Select an Azure Cloud** drop-down, select **AzureUSGovernment**.</span></span>

    ![SSMS Options](./media/documentation-government-connect-with-ssms-img2.png)

3. <span data-ttu-id="89461-122">Browse to **File** > **Connect Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="89461-122">Browse to **File** > **Connect Object Explorer**.</span></span> <span data-ttu-id="89461-123">Enter the name of your computer that's running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89461-123">Enter the name of your computer that's running SQL Server.</span></span> <span data-ttu-id="89461-124">Enter your authentication information.</span><span class="sxs-lookup"><span data-stu-id="89461-124">Enter your authentication information.</span></span> 

    >[!Note]
    ><span data-ttu-id="89461-125">The name of the computer that's running SQL Server ends with **.usgovcloudapi.net**.</span><span class="sxs-lookup"><span data-stu-id="89461-125">The name of the computer that's running SQL Server ends with **.usgovcloudapi.net**.</span></span>
    >
    >

    ![Connect to a computer that's running SQL Server](./media/documentation-government-connect-with-ssms-img3.png)

<span data-ttu-id="89461-127">SSMS is now connected to your Azure Government subscription.</span><span class="sxs-lookup"><span data-stu-id="89461-127">SSMS is now connected to your Azure Government subscription.</span></span>

## <a name="get-help-and-provide-feedback"></a><span data-ttu-id="89461-128">Get help and provide feedback</span><span class="sxs-lookup"><span data-stu-id="89461-128">Get help and provide feedback</span></span>

* <span data-ttu-id="89461-129">Read more about [Azure Storage](https://docs.microsoft.com/azure/storage/).</span><span class="sxs-lookup"><span data-stu-id="89461-129">Read more about [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span> 
* <span data-ttu-id="89461-130">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="89461-130">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>
* <span data-ttu-id="89461-131">Get help on Stack Overflow by using the [`azure-gov`](https://stackoverflow.com/questions/tagged/azure-gov) tag.</span><span class="sxs-lookup"><span data-stu-id="89461-131">Get help on Stack Overflow by using the [`azure-gov`](https://stackoverflow.com/questions/tagged/azure-gov) tag.</span></span>
* <span data-ttu-id="89461-132">Share feedback or request new features by using the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government).</span><span class="sxs-lookup"><span data-stu-id="89461-132">Share feedback or request new features by using the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89461-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="89461-133">Next steps</span></span>

[<span data-ttu-id="89461-134">Develop with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89461-134">Develop with Visual Studio</span></span>](documentation-government-get-started-connect-with-vs.md)