
1. <span data-ttu-id="01b6a-101">To escalate privileges, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-101">To escalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="01b6a-102">Enter your password.</span><span class="sxs-lookup"><span data-stu-id="01b6a-102">Enter your password.</span></span>
2. <span data-ttu-id="01b6a-103">To install MySQL Community Server edition, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-103">To install MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="01b6a-104">Wait while MySQL downloads and installs.</span><span class="sxs-lookup"><span data-stu-id="01b6a-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="01b6a-105">To set MySQL to start when the system boots, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-105">To set MySQL to start when the system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="01b6a-106">Start the MySQL daemon (mysqld) manually with this command:</span><span class="sxs-lookup"><span data-stu-id="01b6a-106">Start the MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="01b6a-107">To check the status of the MySQL daemon, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-107">To check the status of the MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="01b6a-108">To stop the MySQL daemon, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-108">To stop the MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="01b6a-109">After installation, the MySQL root password is empty by default.</span><span class="sxs-lookup"><span data-stu-id="01b6a-109">After installation, the MySQL root password is empty by default.</span></span> <span data-ttu-id="01b6a-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span><span class="sxs-lookup"><span data-stu-id="01b6a-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="01b6a-111">The script prompts you to change the MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload the privileges table.</span><span class="sxs-lookup"><span data-stu-id="01b6a-111">The script prompts you to change the MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload the privileges table.</span></span> <span data-ttu-id="01b6a-112">We recommended that you answer yes to all of these options and change the root password.</span><span class="sxs-lookup"><span data-stu-id="01b6a-112">We recommended that you answer yes to all of these options and change the root password.</span></span>
   > 
   > 
5. <span data-ttu-id="01b6a-113">Type this to run the script MySQL installation script:</span><span class="sxs-lookup"><span data-stu-id="01b6a-113">Type this to run the script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="01b6a-114">Log in to MySQL:</span><span class="sxs-lookup"><span data-stu-id="01b6a-114">Log in to MySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="01b6a-115">Enter the MySQL root password (which you changed in the previous step) and you'll be presented with a prompt where you can issue SQL statements to interact with the database.</span><span class="sxs-lookup"><span data-stu-id="01b6a-115">Enter the MySQL root password (which you changed in the previous step) and you'll be presented with a prompt where you can issue SQL statements to interact with the database.</span></span>
7. <span data-ttu-id="01b6a-116">To create a new MySQL user, run the following at the **mysql>** prompt:</span><span class="sxs-lookup"><span data-stu-id="01b6a-116">To create a new MySQL user, run the following at the **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="01b6a-117">Note, the semi-colons (;) at the end of the lines are crucial for ending the commands.</span><span class="sxs-lookup"><span data-stu-id="01b6a-117">Note, the semi-colons (;) at the end of the lines are crucial for ending the commands.</span></span>
8. <span data-ttu-id="01b6a-118">To create a database and grant the `mysqluser` user permissions on it, issue the following commands:</span><span class="sxs-lookup"><span data-stu-id="01b6a-118">To create a database and grant the `mysqluser` user permissions on it, issue the following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="01b6a-119">Note that database user names and passwords are only used by scripts connecting to the database.</span><span class="sxs-lookup"><span data-stu-id="01b6a-119">Note that database user names and passwords are only used by scripts connecting to the database.</span></span>  <span data-ttu-id="01b6a-120">Database user account names do not necessarily represent actual user accounts on the system.</span><span class="sxs-lookup"><span data-stu-id="01b6a-120">Database user account names do not necessarily represent actual user accounts on the system.</span></span>
9. <span data-ttu-id="01b6a-121">To log in from another computer, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-121">To log in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="01b6a-122">where `ip-address` is the IP address of the computer from which you will connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="01b6a-122">where `ip-address` is the IP address of the computer from which you will connect to MySQL.</span></span>
10. <span data-ttu-id="01b6a-123">To exit the MySQL database administration utility, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-123">To exit the MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="01b6a-124">Add an endpoint</span><span class="sxs-lookup"><span data-stu-id="01b6a-124">Add an endpoint</span></span>
1. <span data-ttu-id="01b6a-125">After MySQL is installed, you'll need to configure an endpoint to access MySQL remotely.</span><span class="sxs-lookup"><span data-stu-id="01b6a-125">After MySQL is installed, you'll need to configure an endpoint to access MySQL remotely.</span></span> <span data-ttu-id="01b6a-126">Log in to the [Azure  classic portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="01b6a-126">Log in to the [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="01b6a-127">Click **Virtual Machines**, click the name of your new virtual machine, and then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="01b6a-127">Click **Virtual Machines**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="01b6a-128">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="01b6a-128">Click **Add** at the bottom of the page.</span></span>
3. <span data-ttu-id="01b6a-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set to "3306".</span><span class="sxs-lookup"><span data-stu-id="01b6a-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set to "3306".</span></span>
4. <span data-ttu-id="01b6a-130">To remotely connect to the virtual machine from your computer, type:</span><span class="sxs-lookup"><span data-stu-id="01b6a-130">To remotely connect to the virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="01b6a-131">For example, using the virual machine we created in this tutorial, type this command:</span><span class="sxs-lookup"><span data-stu-id="01b6a-131">For example, using the virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png

