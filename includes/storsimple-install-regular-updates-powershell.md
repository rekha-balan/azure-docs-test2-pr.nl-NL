<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="d54ed-101">To install regular updates via Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="d54ed-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="d54ed-102">Open the device serial console and select option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="d54ed-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="d54ed-103">Type the password.</span><span class="sxs-lookup"><span data-stu-id="d54ed-103">Type the password.</span></span> <span data-ttu-id="d54ed-104">The default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d54ed-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="d54ed-105">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="d54ed-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="d54ed-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span><span class="sxs-lookup"><span data-stu-id="d54ed-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="d54ed-107">At the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="d54ed-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="d54ed-108">The update process will start.</span><span class="sxs-lookup"><span data-stu-id="d54ed-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d54ed-109">This command applies only to regular updates.</span><span class="sxs-lookup"><span data-stu-id="d54ed-109">This command applies only to regular updates.</span></span> <span data-ttu-id="d54ed-110">You run this command on only one controller, but both controllers will be updated.</span><span class="sxs-lookup"><span data-stu-id="d54ed-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="d54ed-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span><span class="sxs-lookup"><span data-stu-id="d54ed-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

