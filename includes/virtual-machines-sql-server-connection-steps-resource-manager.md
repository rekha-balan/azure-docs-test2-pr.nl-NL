### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="205ef-101">Configure a DNS Label for the public IP address</span><span class="sxs-lookup"><span data-stu-id="205ef-101">Configure a DNS Label for the public IP address</span></span>
<span data-ttu-id="205ef-102">To connect to the SQL Server Database Engine from the Internet, first configure a DNS Label for your public IP address.</span><span class="sxs-lookup"><span data-stu-id="205ef-102">To connect to the SQL Server Database Engine from the Internet, first configure a DNS Label for your public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="205ef-103">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span><span class="sxs-lookup"><span data-stu-id="205ef-103">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>
> 
> 

<span data-ttu-id="205ef-104">To create a DNS Label, first select **Virtual machines** in the portal.</span><span class="sxs-lookup"><span data-stu-id="205ef-104">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="205ef-105">Select your SQL Server VM to bring up its properties.</span><span class="sxs-lookup"><span data-stu-id="205ef-105">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="205ef-106">In the virtual machine blade, select your **Public IP address.**</span><span class="sxs-lookup"><span data-stu-id="205ef-106">In the virtual machine blade, select your **Public IP address.**</span></span>
   
    ![public ip address](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)
2. <span data-ttu-id="205ef-108">In the properties for your Public IP address, expand **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="205ef-108">In the properties for your Public IP address, expand **Configuration**.</span></span>
3. <span data-ttu-id="205ef-109">Enter a DNS Label name.</span><span class="sxs-lookup"><span data-stu-id="205ef-109">Enter a DNS Label name.</span></span> <span data-ttu-id="205ef-110">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span><span class="sxs-lookup"><span data-stu-id="205ef-110">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>
4. <span data-ttu-id="205ef-111">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="205ef-111">Click the **Save** button.</span></span>
   
    ![dns label](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="205ef-113">Connect to the Database Engine from another computer</span><span class="sxs-lookup"><span data-stu-id="205ef-113">Connect to the Database Engine from another computer</span></span>
1. <span data-ttu-id="205ef-114">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="205ef-114">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span>
2. <span data-ttu-id="205ef-115">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span><span class="sxs-lookup"><span data-stu-id="205ef-115">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="205ef-116">Enter the full DNS name of the virtual machine (determined in the previous task).</span><span class="sxs-lookup"><span data-stu-id="205ef-116">Enter the full DNS name of the virtual machine (determined in the previous task).</span></span>
3. <span data-ttu-id="205ef-117">In the **Authentication** box, select **SQL Server Authentication**.</span><span class="sxs-lookup"><span data-stu-id="205ef-117">In the **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="205ef-118">In the **Login** box, type the name of a valid SQL login.</span><span class="sxs-lookup"><span data-stu-id="205ef-118">In the **Login** box, type the name of a valid SQL login.</span></span>
5. <span data-ttu-id="205ef-119">In the **Password** box, type the password of the login.</span><span class="sxs-lookup"><span data-stu-id="205ef-119">In the **Password** box, type the password of the login.</span></span>
6. <span data-ttu-id="205ef-120">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="205ef-120">Click **Connect**.</span></span>
   
    ![ssms connect](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)




