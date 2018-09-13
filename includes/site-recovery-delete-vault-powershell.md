## <a name="delete-a-recovery-services-vault-powershell"></a><span data-ttu-id="c1925-101">Delete a Recovery Services vault (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c1925-101">Delete a Recovery Services vault (PowerShell)</span></span>

1. <span data-ttu-id="c1925-102">Get the Recovery services vault</span><span class="sxs-lookup"><span data-stu-id="c1925-102">Get the Recovery services vault</span></span>

        $vault = Get-AzureRmRecoveryServicesVault -Name "ContosoVault"

2. <span data-ttu-id="c1925-103">Delete the vault</span><span class="sxs-lookup"><span data-stu-id="c1925-103">Delete the vault</span></span>

        Remove-AzureRmRecoveryServicesVault -Vault $vault

>[!WARNING]
>
> <span data-ttu-id="c1925-104">Use the above command with utmost caution since if you delete any vault by mistake, you will lose all the data.</span><span class="sxs-lookup"><span data-stu-id="c1925-104">Use the above command with utmost caution since if you delete any vault by mistake, you will lose all the data.</span></span> <span data-ttu-id="c1925-105">This is a permanent action and there is no way to reverse it.</span><span class="sxs-lookup"><span data-stu-id="c1925-105">This is a permanent action and there is no way to reverse it.</span></span>  


