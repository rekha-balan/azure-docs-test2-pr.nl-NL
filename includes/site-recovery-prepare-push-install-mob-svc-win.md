### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a><span data-ttu-id="6052a-101">Prepare for a push installation on a Windows computer</span><span class="sxs-lookup"><span data-stu-id="6052a-101">Prepare for a push installation on a Windows computer</span></span>

1. <span data-ttu-id="6052a-102">Ensure that there’s network connectivity between the Windows computer and the process server.</span><span class="sxs-lookup"><span data-stu-id="6052a-102">Ensure that there’s network connectivity between the Windows computer and the process server.</span></span>
2. <span data-ttu-id="6052a-103">Create an account that the process server can use to access the computer.</span><span class="sxs-lookup"><span data-stu-id="6052a-103">Create an account that the process server can use to access the computer.</span></span> <span data-ttu-id="6052a-104">The account should have administrator rights (local or domain).</span><span class="sxs-lookup"><span data-stu-id="6052a-104">The account should have administrator rights (local or domain).</span></span> <span data-ttu-id="6052a-105">(Use this account only for the push installation and for agent updates.)</span><span class="sxs-lookup"><span data-stu-id="6052a-105">(Use this account only for the push installation and for agent updates.)</span></span>

   > [!NOTE]
   > <span data-ttu-id="6052a-106">If you're not using a domain account, disable Remote User Access control on the local computer.</span><span class="sxs-lookup"><span data-stu-id="6052a-106">If you're not using a domain account, disable Remote User Access control on the local computer.</span></span> <span data-ttu-id="6052a-107">To disable Remote User Access control, under the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System registry key, add a new DWORD: **LocalAccountTokenFilterPolicy**.</span><span class="sxs-lookup"><span data-stu-id="6052a-107">To disable Remote User Access control, under the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System registry key, add a new DWORD: **LocalAccountTokenFilterPolicy**.</span></span> <span data-ttu-id="6052a-108">Set the value to **1**.</span><span class="sxs-lookup"><span data-stu-id="6052a-108">Set the value to **1**.</span></span> <span data-ttu-id="6052a-109">To do this at a command prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="6052a-109">To do this at a command prompt, run the following command:</span></span>  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. <span data-ttu-id="6052a-110">In Windows Firewall on the computer you want to protect, select **Allow an app or feature through Firewall**.</span><span class="sxs-lookup"><span data-stu-id="6052a-110">In Windows Firewall on the computer you want to protect, select **Allow an app or feature through Firewall**.</span></span> <span data-ttu-id="6052a-111">Enable **File and Printer Sharing** and **Windows Management Instrumentation (WMI)**.</span><span class="sxs-lookup"><span data-stu-id="6052a-111">Enable **File and Printer Sharing** and **Windows Management Instrumentation (WMI)**.</span></span> <span data-ttu-id="6052a-112">For computers that belong to a domain, you can configure the firewall settings by using a Group Policy object (GPO).</span><span class="sxs-lookup"><span data-stu-id="6052a-112">For computers that belong to a domain, you can configure the firewall settings by using a Group Policy object (GPO).</span></span>

   ![Firewall settings](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. <span data-ttu-id="6052a-114">Add the account that you created in CSPSConfigtool.</span><span class="sxs-lookup"><span data-stu-id="6052a-114">Add the account that you created in CSPSConfigtool.</span></span>
    1.  <span data-ttu-id="6052a-115">Sign in to your configuration server.</span><span class="sxs-lookup"><span data-stu-id="6052a-115">Sign in to your configuration server.</span></span>
    2.  <span data-ttu-id="6052a-116">Open **cspsconfigtool.exe**.</span><span class="sxs-lookup"><span data-stu-id="6052a-116">Open **cspsconfigtool.exe**.</span></span> <span data-ttu-id="6052a-117">(It's available as a shortcut on the desktop and in the %ProgramData%\home\svsystems\bin folder.)</span><span class="sxs-lookup"><span data-stu-id="6052a-117">(It's available as a shortcut on the desktop and in the %ProgramData%\home\svsystems\bin folder.)</span></span>
    3.  <span data-ttu-id="6052a-118">On the **Manage Accounts** tab, select **Add Account**.</span><span class="sxs-lookup"><span data-stu-id="6052a-118">On the **Manage Accounts** tab, select **Add Account**.</span></span>
    4.  <span data-ttu-id="6052a-119">Add the account you created.</span><span class="sxs-lookup"><span data-stu-id="6052a-119">Add the account you created.</span></span>
    5.  <span data-ttu-id="6052a-120">Enter the credentials you use when you enable replication for a computer.</span><span class="sxs-lookup"><span data-stu-id="6052a-120">Enter the credentials you use when you enable replication for a computer.</span></span>
