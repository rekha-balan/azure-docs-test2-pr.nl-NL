---
title: include file
description: include file
services: storsimple
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 06/08/2018
ms.author: alkohli
ms.custom: include file
ms.openlocfilehash: e7f3f80c886f90a8bc3ae8c38e7d101c506439a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867872"
---
<span data-ttu-id="db506-103">To delete a volume container, you must</span><span class="sxs-lookup"><span data-stu-id="db506-103">To delete a volume container, you must</span></span>
 - <span data-ttu-id="db506-104">delete volumes in the volume container.</span><span class="sxs-lookup"><span data-stu-id="db506-104">delete volumes in the volume container.</span></span> <span data-ttu-id="db506-105">If the volume container has associated volumes, take those volumes offline first.</span><span class="sxs-lookup"><span data-stu-id="db506-105">If the volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="db506-106">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="db506-106">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).</span></span> <span data-ttu-id="db506-107">After the volumes are offline, you can delete them.</span><span class="sxs-lookup"><span data-stu-id="db506-107">After the volumes are offline, you can delete them.</span></span> 
 - <span data-ttu-id="db506-108">delete associated backup policies and cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="db506-108">delete associated backup policies and cloud snapshots.</span></span> <span data-ttu-id="db506-109">Check if the volume container has associated backup policies and cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="db506-109">Check if the volume container has associated backup policies and cloud snapshots.</span></span> <span data-ttu-id="db506-110">If so, then [delete the backup policies](../articles/storsimple/storsimple-8000-manage-backup-policies-u2.md#delete-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="db506-110">If so, then [delete the backup policies](../articles/storsimple/storsimple-8000-manage-backup-policies-u2.md#delete-a-backup-policy).</span></span> <span data-ttu-id="db506-111">This will also delete the cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="db506-111">This will also delete the cloud snapshots.</span></span> 
 
<span data-ttu-id="db506-112">When the volume container has no associated volumes, backup policies, and cloud snapshots, you can delete it.</span><span class="sxs-lookup"><span data-stu-id="db506-112">When the volume container has no associated volumes, backup policies, and cloud snapshots, you can delete it.</span></span> <span data-ttu-id="db506-113">Perform the following procedure to delete a volume container.</span><span class="sxs-lookup"><span data-stu-id="db506-113">Perform the following procedure to delete a volume container.</span></span>

#### <a name="to-delete-a-volume-container"></a><span data-ttu-id="db506-114">To delete a volume container</span><span class="sxs-lookup"><span data-stu-id="db506-114">To delete a volume container</span></span>
1. <span data-ttu-id="db506-115">Go to your StorSimple Device Manager service and click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="db506-115">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="db506-116">Select and click the device and then go to **Settings > Manage > Volume containers**.</span><span class="sxs-lookup"><span data-stu-id="db506-116">Select and click the device and then go to **Settings > Manage > Volume containers**.</span></span>

    ![Volume containers blade](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="db506-118">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="db506-118">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span></span>

    ![Delete volume container](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="db506-120">If a volume container has no associated volumes, backup policies, and cloud snapshots, then it can be deleted.</span><span class="sxs-lookup"><span data-stu-id="db506-120">If a volume container has no associated volumes, backup policies, and cloud snapshots, then it can be deleted.</span></span> <span data-ttu-id="db506-121">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span><span class="sxs-lookup"><span data-stu-id="db506-121">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span></span> <span data-ttu-id="db506-122">Click **Delete** to then delete the volume container.</span><span class="sxs-lookup"><span data-stu-id="db506-122">Click **Delete** to then delete the volume container.</span></span>

    ![Confirm deletion](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="db506-124">The list of volume containers is updated to reflect the deleted volume container.</span><span class="sxs-lookup"><span data-stu-id="db506-124">The list of volume containers is updated to reflect the deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


