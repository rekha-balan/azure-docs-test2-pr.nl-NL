### <a name="open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine"></a><span data-ttu-id="82d48-101">Open TCP ports in the Windows firewall for the default instance of the Database Engine</span><span class="sxs-lookup"><span data-stu-id="82d48-101">Open TCP ports in the Windows firewall for the default instance of the Database Engine</span></span>
1. <span data-ttu-id="82d48-102">Connect to the virtual machine with Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="82d48-102">Connect to the virtual machine with Remote Desktop.</span></span> <span data-ttu-id="82d48-103">For detailed instructions on connecting to the VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span><span class="sxs-lookup"><span data-stu-id="82d48-103">For detailed instructions on connecting to the VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span></span>
2. <span data-ttu-id="82d48-104">Once logged in, at the Start screen, type **WF.msc**, and then hit ENTER.</span><span class="sxs-lookup"><span data-stu-id="82d48-104">Once logged in, at the Start screen, type **WF.msc**, and then hit ENTER.</span></span>
   
    ![Start the Firewall Program](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. <span data-ttu-id="82d48-106">In the **Windows Firewall with Advanced Security**, in the left pane, right-click **Inbound Rules**, and then click **New Rule** in the action pane.</span><span class="sxs-lookup"><span data-stu-id="82d48-106">In the **Windows Firewall with Advanced Security**, in the left pane, right-click **Inbound Rules**, and then click **New Rule** in the action pane.</span></span>
   
    ![New Rule](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. <span data-ttu-id="82d48-108">In the **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d48-108">In the **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span></span>
5. <span data-ttu-id="82d48-109">In the **Protocol and Ports** dialog, use the default **TCP**.</span><span class="sxs-lookup"><span data-stu-id="82d48-109">In the **Protocol and Ports** dialog, use the default **TCP**.</span></span> <span data-ttu-id="82d48-110">In the **Specific local ports** box, then type the port number of the instance of the Database Engine (**1433** for the default instance or your choice for the private port in the endpoint step).</span><span class="sxs-lookup"><span data-stu-id="82d48-110">In the **Specific local ports** box, then type the port number of the instance of the Database Engine (**1433** for the default instance or your choice for the private port in the endpoint step).</span></span>
   
    ![TCP Port 1433](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. <span data-ttu-id="82d48-112">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d48-112">Click **Next**.</span></span>
7. <span data-ttu-id="82d48-113">In the **Action** dialog box, select **Allow the connection**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d48-113">In the **Action** dialog box, select **Allow the connection**, and then click **Next**.</span></span>
   
    <span data-ttu-id="82d48-114">**Security Note:** Selecting **Allow the connection if it is secure** can provide additional security.</span><span class="sxs-lookup"><span data-stu-id="82d48-114">**Security Note:** Selecting **Allow the connection if it is secure** can provide additional security.</span></span> <span data-ttu-id="82d48-115">Select this option if you want to configure additional security options in your environment.</span><span class="sxs-lookup"><span data-stu-id="82d48-115">Select this option if you want to configure additional security options in your environment.</span></span>
   
    ![Allow Connections](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. <span data-ttu-id="82d48-117">In the **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span><span class="sxs-lookup"><span data-stu-id="82d48-117">In the **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span></span> <span data-ttu-id="82d48-118">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="82d48-118">Then click **Next**.</span></span>
   
    <span data-ttu-id="82d48-119">**Security Note:**  Selecting **Public** allows access over the internet.</span><span class="sxs-lookup"><span data-stu-id="82d48-119">**Security Note:**  Selecting **Public** allows access over the internet.</span></span> <span data-ttu-id="82d48-120">Whenever possible, select a more restrictive profile.</span><span class="sxs-lookup"><span data-stu-id="82d48-120">Whenever possible, select a more restrictive profile.</span></span>
   
    ![Public Profile](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. <span data-ttu-id="82d48-122">In the **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="82d48-122">In the **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span></span>
   
    ![Rule Name](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

<span data-ttu-id="82d48-124">Open additional ports for other components as needed.</span><span class="sxs-lookup"><span data-stu-id="82d48-124">Open additional ports for other components as needed.</span></span> <span data-ttu-id="82d48-125">For more information, see [Configuring the Windows Firewall to Allow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span><span class="sxs-lookup"><span data-stu-id="82d48-125">For more information, see [Configuring the Windows Firewall to Allow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span></span>

### <a name="configure-sql-server-to-listen-on-the-tcp-protocol"></a><span data-ttu-id="82d48-126">Configure SQL Server to listen on the TCP protocol</span><span class="sxs-lookup"><span data-stu-id="82d48-126">Configure SQL Server to listen on the TCP protocol</span></span>
1. <span data-ttu-id="82d48-127">While connected to the virtual machine, on the Start page, type **SQL Server Configuration Manager** and hit ENTER.</span><span class="sxs-lookup"><span data-stu-id="82d48-127">While connected to the virtual machine, on the Start page, type **SQL Server Configuration Manager** and hit ENTER.</span></span>
   
    ![Open SSCM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/9Click-SSCM.png)
2. <span data-ttu-id="82d48-129">In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**.</span><span class="sxs-lookup"><span data-stu-id="82d48-129">In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**.</span></span>
3. <span data-ttu-id="82d48-130">In the console pane, click **Protocols for MSSQLSERVER** (he default instance name.) In the details pane, right-click **TCP** and click **Enable** if it is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="82d48-130">In the console pane, click **Protocols for MSSQLSERVER** (he default instance name.) In the details pane, right-click **TCP** and click **Enable** if it is not already enabled.</span></span>
   
    ![Enable TCP](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/10Enable-TCP.png)
4. <span data-ttu-id="82d48-132">In the console pane, click **SQL Server Services**.</span><span class="sxs-lookup"><span data-stu-id="82d48-132">In the console pane, click **SQL Server Services**.</span></span> <span data-ttu-id="82d48-133">In the details pane, right-click **SQL Server (*instance name*)** (the default instance is **SQL Server (MSSQLSERVER)**), and then click **Restart**, to stop and restart the instance of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82d48-133">In the details pane, right-click **SQL Server (*instance name*)** (the default instance is **SQL Server (MSSQLSERVER)**), and then click **Restart**, to stop and restart the instance of SQL Server.</span></span>
   
    ![Restart Database Engine](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/11Restart.png)
5. <span data-ttu-id="82d48-135">Close SQL Server Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="82d48-135">Close SQL Server Configuration Manager.</span></span>

<span data-ttu-id="82d48-136">For more information about enabling protocols for the SQL Server Database Engine, see [Enable or Disable a Server Network Protocol](http://msdn.microsoft.com/library/ms191294.aspx).</span><span class="sxs-lookup"><span data-stu-id="82d48-136">For more information about enabling protocols for the SQL Server Database Engine, see [Enable or Disable a Server Network Protocol](http://msdn.microsoft.com/library/ms191294.aspx).</span></span>

### <a name="configure-sql-server-for-mixed-mode-authentication"></a><span data-ttu-id="82d48-137">Configure SQL Server for mixed mode authentication</span><span class="sxs-lookup"><span data-stu-id="82d48-137">Configure SQL Server for mixed mode authentication</span></span>
<span data-ttu-id="82d48-138">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span><span class="sxs-lookup"><span data-stu-id="82d48-138">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="82d48-139">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span><span class="sxs-lookup"><span data-stu-id="82d48-139">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="82d48-140">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="82d48-140">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="82d48-141">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span><span class="sxs-lookup"><span data-stu-id="82d48-141">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span></span>
> 
> 

1. <span data-ttu-id="82d48-142">While connected to the virtual machine, on the Start page, type **SQL Server Management Studio** and click the selected icon.</span><span class="sxs-lookup"><span data-stu-id="82d48-142">While connected to the virtual machine, on the Start page, type **SQL Server Management Studio** and click the selected icon.</span></span>
   
    <span data-ttu-id="82d48-143">The first time you open Management Studio it must create the users Management Studio environment.</span><span class="sxs-lookup"><span data-stu-id="82d48-143">The first time you open Management Studio it must create the users Management Studio environment.</span></span> <span data-ttu-id="82d48-144">This may take a few moments.</span><span class="sxs-lookup"><span data-stu-id="82d48-144">This may take a few moments.</span></span>
2. <span data-ttu-id="82d48-145">Management Studio presents the **Connect to Server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="82d48-145">Management Studio presents the **Connect to Server** dialog box.</span></span> <span data-ttu-id="82d48-146">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine  with the Object Explorer (Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**).</span><span class="sxs-lookup"><span data-stu-id="82d48-146">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine  with the Object Explorer (Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**).</span></span> <span data-ttu-id="82d48-147">Select **Windows Authentication**, and leave \***your_VM_name\*\your_local_administrator** in the **User name** box.</span><span class="sxs-lookup"><span data-stu-id="82d48-147">Select **Windows Authentication**, and leave \***your_VM_name\*\your_local_administrator** in the **User name** box.</span></span> <span data-ttu-id="82d48-148">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="82d48-148">Click **Connect**.</span></span>
   
    ![Connect to Server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. <span data-ttu-id="82d48-150">In SQL Server Management Studio Object Explorer, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="82d48-150">In SQL Server Management Studio Object Explorer, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span></span>
   
    ![Server Properties](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. <span data-ttu-id="82d48-152">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82d48-152">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
    ![Select Authentication Mode](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. <span data-ttu-id="82d48-154">In the SQL Server Management Studio dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82d48-154">In the SQL Server Management Studio dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span></span>
6. <span data-ttu-id="82d48-155">In Object Explorer, right-click your server, and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="82d48-155">In Object Explorer, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="82d48-156">(If SQL Server Agent is running, it must also be restarted.)</span><span class="sxs-lookup"><span data-stu-id="82d48-156">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
    ![Restart](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. <span data-ttu-id="82d48-158">In the SQL Server Management Studio dialog box, click **Yes** to agree that you want to restart SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82d48-158">In the SQL Server Management Studio dialog box, click **Yes** to agree that you want to restart SQL Server.</span></span>

### <a name="create-sql-server-authentication-logins"></a><span data-ttu-id="82d48-159">Create SQL Server authentication logins</span><span class="sxs-lookup"><span data-stu-id="82d48-159">Create SQL Server authentication logins</span></span>
<span data-ttu-id="82d48-160">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span><span class="sxs-lookup"><span data-stu-id="82d48-160">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>

1. <span data-ttu-id="82d48-161">In SQL Server Management Studio Object Explorer, expand the folder of the server instance in which you want to create the new login.</span><span class="sxs-lookup"><span data-stu-id="82d48-161">In SQL Server Management Studio Object Explorer, expand the folder of the server instance in which you want to create the new login.</span></span>
2. <span data-ttu-id="82d48-162">Right-click the **Security** folder, point to **New**, and select **Login...**.</span><span class="sxs-lookup"><span data-stu-id="82d48-162">Right-click the **Security** folder, point to **New**, and select **Login...**.</span></span>
   
    ![New Login](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. <span data-ttu-id="82d48-164">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span><span class="sxs-lookup"><span data-stu-id="82d48-164">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span></span>
4. <span data-ttu-id="82d48-165">Select **SQL Server authentication**.</span><span class="sxs-lookup"><span data-stu-id="82d48-165">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="82d48-166">In the **Password** box, enter a password for the new user.</span><span class="sxs-lookup"><span data-stu-id="82d48-166">In the **Password** box, enter a password for the new user.</span></span> <span data-ttu-id="82d48-167">Enter that password again into the **Confirm Password** box.</span><span class="sxs-lookup"><span data-stu-id="82d48-167">Enter that password again into the **Confirm Password** box.</span></span>
6. <span data-ttu-id="82d48-168">Select the password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span><span class="sxs-lookup"><span data-stu-id="82d48-168">Select the password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span></span> <span data-ttu-id="82d48-169">If you are using this login for yourself, you do not need to require a password change at the next login.</span><span class="sxs-lookup"><span data-stu-id="82d48-169">If you are using this login for yourself, you do not need to require a password change at the next login.</span></span>
7. <span data-ttu-id="82d48-170">From the **Default database** list, select a default database for the login.</span><span class="sxs-lookup"><span data-stu-id="82d48-170">From the **Default database** list, select a default database for the login.</span></span> <span data-ttu-id="82d48-171">**master** is the default for this option.</span><span class="sxs-lookup"><span data-stu-id="82d48-171">**master** is the default for this option.</span></span> <span data-ttu-id="82d48-172">If you have not yet created a user database, leave this set to **master**.</span><span class="sxs-lookup"><span data-stu-id="82d48-172">If you have not yet created a user database, leave this set to **master**.</span></span>
   
    ![Login Properties](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. <span data-ttu-id="82d48-174">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span><span class="sxs-lookup"><span data-stu-id="82d48-174">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="82d48-175">If so, on the **Server Roles** page, check **sysadmin**.</span><span class="sxs-lookup"><span data-stu-id="82d48-175">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="82d48-176">Members of the sysadmin fixed server role have complete control of the Database Engine.</span><span class="sxs-lookup"><span data-stu-id="82d48-176">Members of the sysadmin fixed server role have complete control of the Database Engine.</span></span> <span data-ttu-id="82d48-177">You should carefully restrict membership in this role.</span><span class="sxs-lookup"><span data-stu-id="82d48-177">You should carefully restrict membership in this role.</span></span>
   > 
   > 
   
   ![sysadmin](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. <span data-ttu-id="82d48-179">Click OK.</span><span class="sxs-lookup"><span data-stu-id="82d48-179">Click OK.</span></span>

<span data-ttu-id="82d48-180">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span><span class="sxs-lookup"><span data-stu-id="82d48-180">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>

















