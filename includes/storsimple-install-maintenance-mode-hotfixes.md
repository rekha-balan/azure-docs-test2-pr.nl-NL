<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="512fc-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="512fc-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="512fc-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span><span class="sxs-lookup"><span data-stu-id="512fc-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span></span>
> 
> 

1. <span data-ttu-id="512fc-103">Place the device into Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="512fc-103">Place the device into Maintenance mode.</span></span> <span data-ttu-id="512fc-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="512fc-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span></span>
2. <span data-ttu-id="512fc-105">To apply the hotfix, type:</span><span class="sxs-lookup"><span data-stu-id="512fc-105">To apply the hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="512fc-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span><span class="sxs-lookup"><span data-stu-id="512fc-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
4. <span data-ttu-id="512fc-107">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="512fc-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="512fc-108">Type **Y** to proceed with the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="512fc-108">Type **Y** to proceed with the hotfix installation.</span></span>
5. <span data-ttu-id="512fc-109">After you have applied the hotfix on one controller, log on to the other controller.</span><span class="sxs-lookup"><span data-stu-id="512fc-109">After you have applied the hotfix on one controller, log on to the other controller.</span></span> <span data-ttu-id="512fc-110">Apply the hotfix as you did for the previous controller.</span><span class="sxs-lookup"><span data-stu-id="512fc-110">Apply the hotfix as you did for the previous controller.</span></span>
6. <span data-ttu-id="512fc-111">After the hotfixes are applied, exit Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="512fc-111">After the hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="512fc-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span><span class="sxs-lookup"><span data-stu-id="512fc-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

