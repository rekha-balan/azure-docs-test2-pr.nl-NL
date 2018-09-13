## <a name="install-wordpress"></a><span data-ttu-id="c3d32-101">Install WordPress</span><span class="sxs-lookup"><span data-stu-id="c3d32-101">Install WordPress</span></span>

<span data-ttu-id="c3d32-102">If you want to try your stack, install a sample app.</span><span class="sxs-lookup"><span data-stu-id="c3d32-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="c3d32-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span><span class="sxs-lookup"><span data-stu-id="c3d32-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="c3d32-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="c3d32-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="c3d32-105">This WordPress setup is only for proof of concept.</span><span class="sxs-lookup"><span data-stu-id="c3d32-105">This WordPress setup is only for proof of concept.</span></span> <span data-ttu-id="c3d32-106">To install the latest WordPress in production with recommended security settings, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="c3d32-106">To install the latest WordPress in production with recommended security settings, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="c3d32-107">Install the WordPress package</span><span class="sxs-lookup"><span data-stu-id="c3d32-107">Install the WordPress package</span></span>

<span data-ttu-id="c3d32-108">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="c3d32-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="c3d32-109">Configure WordPress</span><span class="sxs-lookup"><span data-stu-id="c3d32-109">Configure WordPress</span></span>

<span data-ttu-id="c3d32-110">Configure WordPress to use MySQL and PHP.</span><span class="sxs-lookup"><span data-stu-id="c3d32-110">Configure WordPress to use MySQL and PHP.</span></span>

<span data-ttu-id="c3d32-111">In a working directory, create a text file `wordpress.sql` to configure the MySQL database for WordPress:</span><span class="sxs-lookup"><span data-stu-id="c3d32-111">In a working directory, create a text file `wordpress.sql` to configure the MySQL database for WordPress:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="c3d32-112">Add the following commands, substituting a database password of your choice for *yourPassword* (leave other values unchanged).</span><span class="sxs-lookup"><span data-stu-id="c3d32-112">Add the following commands, substituting a database password of your choice for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="c3d32-113">If you previously set up a MySQL security policy to validate password strength, make sure the password meets the strength requirements.</span><span class="sxs-lookup"><span data-stu-id="c3d32-113">If you previously set up a MySQL security policy to validate password strength, make sure the password meets the strength requirements.</span></span> <span data-ttu-id="c3d32-114">Save the file.</span><span class="sxs-lookup"><span data-stu-id="c3d32-114">Save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```

<span data-ttu-id="c3d32-115">Run the following command to create the database:</span><span class="sxs-lookup"><span data-stu-id="c3d32-115">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="c3d32-116">Because the file `wordpress.sql` contains database credentials, delete it after use:</span><span class="sxs-lookup"><span data-stu-id="c3d32-116">Because the file `wordpress.sql` contains database credentials, delete it after use:</span></span>

```bash
sudo rm wordpress.sql
```

<span data-ttu-id="c3d32-117">To configure PHP, run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="c3d32-117">To configure PHP, run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="c3d32-118">Copy the following lines to the file, substituting your WordPress database password for *yourPassword* (leave other values unchanged).</span><span class="sxs-lookup"><span data-stu-id="c3d32-118">Copy the following lines to the file, substituting your WordPress database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="c3d32-119">Then save the file.</span><span class="sxs-lookup"><span data-stu-id="c3d32-119">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```


<span data-ttu-id="c3d32-120">Move the WordPress installation to the web server document root:</span><span class="sxs-lookup"><span data-stu-id="c3d32-120">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="c3d32-121">Now you can complete the WordPress setup and publish on the platform.</span><span class="sxs-lookup"><span data-stu-id="c3d32-121">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="c3d32-122">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="c3d32-122">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="c3d32-123">Substitute the public IP address of your VM.</span><span class="sxs-lookup"><span data-stu-id="c3d32-123">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="c3d32-124">It should look similar to this image.</span><span class="sxs-lookup"><span data-stu-id="c3d32-124">It should look similar to this image.</span></span>

![WordPress installation page](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)