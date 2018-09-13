<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="e8c39-101">To install regular hotfixes via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="e8c39-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="e8c39-102">Connect to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="e8c39-102">Connect to the device serial console.</span></span> <span data-ttu-id="e8c39-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="e8c39-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="e8c39-104">In the serial console menu, select option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="e8c39-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="e8c39-105">Type the password.</span><span class="sxs-lookup"><span data-stu-id="e8c39-105">Type the password.</span></span> <span data-ttu-id="e8c39-106">The default password is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="e8c39-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="e8c39-107">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="e8c39-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="e8c39-108">This command applies only to regular hotfixes.</span><span class="sxs-lookup"><span data-stu-id="e8c39-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="e8c39-109">You run this command on only one controller, but both controllers will be updated.</span><span class="sxs-lookup"><span data-stu-id="e8c39-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="e8c39-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span><span class="sxs-lookup"><span data-stu-id="e8c39-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="e8c39-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span><span class="sxs-lookup"><span data-stu-id="e8c39-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="e8c39-112">You will be prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="e8c39-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="e8c39-113">Type **Y** to proceed with the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="e8c39-113">Type **Y** to proceed with the hotfix installation.</span></span>

