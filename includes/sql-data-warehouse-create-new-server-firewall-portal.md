### <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="86d8d-101">Create a server-level firewall rule in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="86d8d-101">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="86d8d-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span><span class="sxs-lookup"><span data-stu-id="86d8d-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span></span>

    ![sql server firewall](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-server-firewall/sql-server-firewall.png)
    
2. <span data-ttu-id="86d8d-104">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span><span class="sxs-lookup"><span data-stu-id="86d8d-104">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="86d8d-105">Occasionally they do not match for a various reasons.</span><span class="sxs-lookup"><span data-stu-id="86d8d-105">Occasionally they do not match for a various reasons.</span></span>

    ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png)

3. <span data-ttu-id="86d8d-107">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="86d8d-107">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span></span>

    ![add client IP](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-server-firewall/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="86d8d-109">You can open the firewall on the SQL server (logical server) to a single IP address or an entire range of addresses.</span><span class="sxs-lookup"><span data-stu-id="86d8d-109">You can open the firewall on the SQL server (logical server) to a single IP address or an entire range of addresses.</span></span> <span data-ttu-id="86d8d-110">Opening the firewall enables SQL administrators and users to login to any database on the server for which they have valid credentials.</span><span class="sxs-lookup"><span data-stu-id="86d8d-110">Opening the firewall enables SQL administrators and users to login to any database on the server for which they have valid credentials.</span></span>
    >

4. <span data-ttu-id="86d8d-111">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="86d8d-111">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span></span>

    ![add client IP](../articles/sql-database/media/sql-database-get-started/save-firewall-rule.png)

