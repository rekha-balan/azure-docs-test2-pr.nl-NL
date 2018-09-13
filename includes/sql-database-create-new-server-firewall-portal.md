
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, the following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="c8723-101">Create a server-level firewall rule in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8723-101">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="c8723-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span><span class="sxs-lookup"><span data-stu-id="c8723-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="c8723-103">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span><span class="sxs-lookup"><span data-stu-id="c8723-103">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="c8723-104">Occasionally they do not match for a various reasons.</span><span class="sxs-lookup"><span data-stu-id="c8723-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="c8723-105">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="c8723-105">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span></span>

    ![add client IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="c8723-107">You can open the SQL Database firewall on the server to a single IP address or an entire range of addresses.</span><span class="sxs-lookup"><span data-stu-id="c8723-107">You can open the SQL Database firewall on the server to a single IP address or an entire range of addresses.</span></span> <span data-ttu-id="c8723-108">Opening the firewall enables SQL administrators and users to login to any database on the server to which they have valid credentials.</span><span class="sxs-lookup"><span data-stu-id="c8723-108">Opening the firewall enables SQL administrators and users to login to any database on the server to which they have valid credentials.</span></span>
    >

4. <span data-ttu-id="c8723-109">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8723-109">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span></span>

    ![add client IP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="c8723-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8723-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>


