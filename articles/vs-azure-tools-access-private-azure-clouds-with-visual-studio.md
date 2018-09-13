---
title: Accessing private Azure clouds with Visual Studio | Microsoft Docs
description: Learn how to access private cloud resources by using Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: tarcher
ms.openlocfilehash: 781f4b11a7345bb07ff2b5e88090b3bcdafc4b2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549731"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="3a1be-103">Accessing private Azure clouds with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a1be-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="3a1be-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span><span class="sxs-lookup"><span data-stu-id="3a1be-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="3a1be-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a1be-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="3a1be-106">To access a private Azure cloud in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a1be-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="3a1be-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span><span class="sxs-lookup"><span data-stu-id="3a1be-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="3a1be-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="3a1be-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="3a1be-109">(The downloaded file should have an extension of `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="3a1be-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="3a1be-110">Open Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a1be-110">Open Visual Studio</span></span>

1. <span data-ttu-id="3a1be-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="3a1be-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Manage subscriptions command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="3a1be-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span><span class="sxs-lookup"><span data-stu-id="3a1be-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importing Azure certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="3a1be-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="3a1be-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Browse button on the Import Microsoft Azure Subscriptions dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="3a1be-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="3a1be-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Select the publish-settings file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="3a1be-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span><span class="sxs-lookup"><span data-stu-id="3a1be-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Import the publish-settings file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="3a1be-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span><span class="sxs-lookup"><span data-stu-id="3a1be-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="3a1be-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a1be-122">Next steps</span></span>
- [<span data-ttu-id="3a1be-123">Publishing to an Azure Cloud Service from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a1be-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="3a1be-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="3a1be-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>





