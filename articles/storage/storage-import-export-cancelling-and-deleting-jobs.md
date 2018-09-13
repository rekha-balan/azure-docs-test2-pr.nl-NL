---
title: Cancel and delete an Azure Import/Export job | Microsoft Docs
description: Learn how to cancel and delete jobs for the Microsoft Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553190"
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="e5ae4-103">Canceling and deleting Azure Import/Export jobs</span><span class="sxs-lookup"><span data-stu-id="e5ae4-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="e5ae4-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="e5ae4-105">The job will be cancelled on a best-effort basis.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="e5ae4-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="e5ae4-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="e5ae4-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span><span class="sxs-lookup"><span data-stu-id="e5ae4-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="e5ae4-109">You can also delete a job when it is in the `Completed` state.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="e5ae4-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5ae4-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5ae4-111">Next steps</span></span>

* [<span data-ttu-id="e5ae4-112">Using the Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="e5ae4-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
