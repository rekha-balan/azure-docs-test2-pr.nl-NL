
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="448a5-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="448a5-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="448a5-102">In the left banner, click **BROWSE ALL**.</span><span class="sxs-lookup"><span data-stu-id="448a5-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="448a5-103">The **Browse** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="448a5-104">Scroll and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="448a5-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="448a5-105">The **SQL servers** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Find your Azure SQL Database server in the portal][b21-FindServerInPortal]
4. <span data-ttu-id="448a5-107">For convenience, click the minimize control on the earlier **Browse** blade.</span><span class="sxs-lookup"><span data-stu-id="448a5-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="448a5-108">In the filter text box, start typing the name of your server.</span><span class="sxs-lookup"><span data-stu-id="448a5-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="448a5-109">Your row is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-109">Your row is displayed.</span></span>
6. <span data-ttu-id="448a5-110">Click the row for your server.</span><span class="sxs-lookup"><span data-stu-id="448a5-110">Click the row for your server.</span></span> <span data-ttu-id="448a5-111">A blade for your server is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="448a5-112">On your server blade, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="448a5-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="448a5-113">The **Settings** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="448a5-114">Click **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="448a5-114">Click **Firewall**.</span></span> <span data-ttu-id="448a5-115">The **Firewall Settings** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="448a5-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Click Settings > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="448a5-117">Click **Add Client IP**.</span><span class="sxs-lookup"><span data-stu-id="448a5-117">Click **Add Client IP**.</span></span> <span data-ttu-id="448a5-118">Type in a name for your new rule into the first text box.</span><span class="sxs-lookup"><span data-stu-id="448a5-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="448a5-119">Type in the low and high IP address values for the range you want to enable.</span><span class="sxs-lookup"><span data-stu-id="448a5-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="448a5-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span><span class="sxs-lookup"><span data-stu-id="448a5-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Add an IP address range to allow][b41-AddRange]
11. <span data-ttu-id="448a5-122">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="448a5-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->



