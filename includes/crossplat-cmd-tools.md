# <a name="how-to-use-the-azure-command-line-tools-for-mac-and-linux"></a><span data-ttu-id="51b46-101">How to use the Azure Command-Line Tools for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="51b46-101">How to use the Azure Command-Line Tools for Mac and Linux</span></span>
<span data-ttu-id="51b46-102">This guide describes how to use the Azure Command-Line Tools for Mac and Linux to create and manage services in Azure.</span><span class="sxs-lookup"><span data-stu-id="51b46-102">This guide describes how to use the Azure Command-Line Tools for Mac and Linux to create and manage services in Azure.</span></span> <span data-ttu-id="51b46-103">The scenarios covered include **installing the tools**, **importing your publishing settings**, **creating and managing Azure Websites**, and **creating and managing Azure Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="51b46-103">The scenarios covered include **installing the tools**, **importing your publishing settings**, **creating and managing Azure Websites**, and **creating and managing Azure Virtual Machines**.</span></span> <span data-ttu-id="51b46-104">For comprehensive reference documentation, see [Azure command-line tool for Mac and Linux Documentation][reference-docs].</span><span class="sxs-lookup"><span data-stu-id="51b46-104">For comprehensive reference documentation, see [Azure command-line tool for Mac and Linux Documentation][reference-docs].</span></span> 

## <a name="table-of-contents"></a><span data-ttu-id="51b46-105">Table of contents</span><span class="sxs-lookup"><span data-stu-id="51b46-105">Table of contents</span></span>
* [<span data-ttu-id="51b46-106">What are the Azure Command-Line Tools for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="51b46-106">What are the Azure Command-Line Tools for Mac and Linux</span></span>](#Overview)
* [<span data-ttu-id="51b46-107">How to install the Azure Command-Line Tools for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="51b46-107">How to install the Azure Command-Line Tools for Mac and Linux</span></span>](#Download)
* [<span data-ttu-id="51b46-108">How to create an Azure account</span><span class="sxs-lookup"><span data-stu-id="51b46-108">How to create an Azure account</span></span>](#CreateAccount)
* [<span data-ttu-id="51b46-109">How to download and import publish settings</span><span class="sxs-lookup"><span data-stu-id="51b46-109">How to download and import publish settings</span></span>](#Account)
* [<span data-ttu-id="51b46-110">How to create and manage an Azure Web Site</span><span class="sxs-lookup"><span data-stu-id="51b46-110">How to create and manage an Azure Web Site</span></span>](#WebSites)
* [<span data-ttu-id="51b46-111">How to create and manage an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="51b46-111">How to create and manage an Azure Virtual Machine</span></span>](#VMs)

<h2><a id="Overview"></a><span data-ttu-id="51b46-112">What are the Azure Command-Line Tools for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="51b46-112">What are the Azure Command-Line Tools for Mac and Linux</span></span></h2>

<span data-ttu-id="51b46-113">The Azure Command-Line Tools for Mac and Linux are a set of command-line tools for deploying and managing Azure services.</span><span class="sxs-lookup"><span data-stu-id="51b46-113">The Azure Command-Line Tools for Mac and Linux are a set of command-line tools for deploying and managing Azure services.</span></span>

<span data-ttu-id="51b46-114">The supported tasks include the following:</span><span class="sxs-lookup"><span data-stu-id="51b46-114">The supported tasks include the following:</span></span>

* <span data-ttu-id="51b46-115">Import publishing settings.</span><span class="sxs-lookup"><span data-stu-id="51b46-115">Import publishing settings.</span></span>
* <span data-ttu-id="51b46-116">Create and manage Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="51b46-116">Create and manage Azure Websites.</span></span>
* <span data-ttu-id="51b46-117">Create and manage Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="51b46-117">Create and manage Azure Virtual Machines.</span></span>

<span data-ttu-id="51b46-118">For a complete list of supported commands, type `azure -help` at the command line after installing the tools, or see the [reference documentation][reference-docs].</span><span class="sxs-lookup"><span data-stu-id="51b46-118">For a complete list of supported commands, type `azure -help` at the command line after installing the tools, or see the [reference documentation][reference-docs].</span></span>

<h2><span data-ttu-id="51b46-119"><a id="Download">How to install the Azure Command-Line Tools for Mac and Linux</a></span><span class="sxs-lookup"><span data-stu-id="51b46-119"><a id="Download">How to install the Azure Command-Line Tools for Mac and Linux</a></span></span></h2>

<span data-ttu-id="51b46-120">The following list contains information for installing the command-line tools, depending on your operating system:</span><span class="sxs-lookup"><span data-stu-id="51b46-120">The following list contains information for installing the command-line tools, depending on your operating system:</span></span>

* <span data-ttu-id="51b46-121">**Mac**: Download the [Azure SDK Installer][mac-installer].</span><span class="sxs-lookup"><span data-stu-id="51b46-121">**Mac**: Download the [Azure SDK Installer][mac-installer].</span></span> <span data-ttu-id="51b46-122">Open the downloaded .pkg file and complete the installation steps as you are prompted.</span><span class="sxs-lookup"><span data-stu-id="51b46-122">Open the downloaded .pkg file and complete the installation steps as you are prompted.</span></span>
* <span data-ttu-id="51b46-123">**Linux**: Install the latest version of [Node.js][nodejs-org] (see [Install Node.js via Package Manager][install-node-linux]), then run the following command:</span><span class="sxs-lookup"><span data-stu-id="51b46-123">**Linux**: Install the latest version of [Node.js][nodejs-org] (see [Install Node.js via Package Manager][install-node-linux]), then run the following command:</span></span>
  
        npm install azure-cli -g
  
    <span data-ttu-id="51b46-124">**Note**: You may need to run this command with elevated privileges:</span><span class="sxs-lookup"><span data-stu-id="51b46-124">**Note**: You may need to run this command with elevated privileges:</span></span>
  
        sudo npm install azure-cli -g
* <span data-ttu-id="51b46-125">**Windows**: Run the Winows installer (.msi file), which is available here: [Azure Command Line Tools][windows-installer].</span><span class="sxs-lookup"><span data-stu-id="51b46-125">**Windows**: Run the Winows installer (.msi file), which is available here: [Azure Command Line Tools][windows-installer].</span></span>

<span data-ttu-id="51b46-126">To test the installation, type `azure` at the command prompt.</span><span class="sxs-lookup"><span data-stu-id="51b46-126">To test the installation, type `azure` at the command prompt.</span></span> <span data-ttu-id="51b46-127">If the installation was successful, you will see a list of all the available `azure` commands.</span><span class="sxs-lookup"><span data-stu-id="51b46-127">If the installation was successful, you will see a list of all the available `azure` commands.</span></span>

<h2><a id="CreateAccount"></a><span data-ttu-id="51b46-128">How to create an Azure account</span><span class="sxs-lookup"><span data-stu-id="51b46-128">How to create an Azure account</span></span></h2>

<span data-ttu-id="51b46-129">To use the Azure Command-Line Tools for Mac and Linux, you will need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="51b46-129">To use the Azure Command-Line Tools for Mac and Linux, you will need an Azure account.</span></span>

<span data-ttu-id="51b46-130">Open a web browser and browse to [http://www.windowsazure.com][windowsazuredotcom] and click **free account** in the upper right corner.</span><span class="sxs-lookup"><span data-stu-id="51b46-130">Open a web browser and browse to [http://www.windowsazure.com][windowsazuredotcom] and click **free account** in the upper right corner.</span></span>

![Azure Web Site][Azure Web Site]

<span data-ttu-id="51b46-132">Follow the instructions for creating an account.</span><span class="sxs-lookup"><span data-stu-id="51b46-132">Follow the instructions for creating an account.</span></span>

<h2><a id="Account"></a><span data-ttu-id="51b46-133">How to download and import publish settings</span><span class="sxs-lookup"><span data-stu-id="51b46-133">How to download and import publish settings</span></span></h2>

<span data-ttu-id="51b46-134">To get started, you need to first download and import your publish settings.</span><span class="sxs-lookup"><span data-stu-id="51b46-134">To get started, you need to first download and import your publish settings.</span></span> <span data-ttu-id="51b46-135">This will allow you to use the tools to create and manage Azure Services.</span><span class="sxs-lookup"><span data-stu-id="51b46-135">This will allow you to use the tools to create and manage Azure Services.</span></span> <span data-ttu-id="51b46-136">To download your publish settings, use the `account download` command:</span><span class="sxs-lookup"><span data-stu-id="51b46-136">To download your publish settings, use the `account download` command:</span></span>

    azure account download

<span data-ttu-id="51b46-137">This will open your default browser and prompt you to sign in to the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="51b46-137">This will open your default browser and prompt you to sign in to the Management Portal.</span></span> <span data-ttu-id="51b46-138">After signing in, your `.publishsettings` file will be downloaded.</span><span class="sxs-lookup"><span data-stu-id="51b46-138">After signing in, your `.publishsettings` file will be downloaded.</span></span> <span data-ttu-id="51b46-139">Make note of where this file is saved.</span><span class="sxs-lookup"><span data-stu-id="51b46-139">Make note of where this file is saved.</span></span>

<span data-ttu-id="51b46-140">Next, import the `.publishsettings` file by running the following command, replacing `{path to .publishsettings file}` with the path to your `.publishsettings` file:</span><span class="sxs-lookup"><span data-stu-id="51b46-140">Next, import the `.publishsettings` file by running the following command, replacing `{path to .publishsettings file}` with the path to your `.publishsettings` file:</span></span>

    azure account import {path to .publishsettings file}

<span data-ttu-id="51b46-141">You can remove all of the information stored by the <code>import</code> command by using the <code>account clear</code> command:</span><span class="sxs-lookup"><span data-stu-id="51b46-141">You can remove all of the information stored by the <code>import</code> command by using the <code>account clear</code> command:</span></span>

    azure account clear

<span data-ttu-id="51b46-142">To see a list of options for `account` commands, use the `-help` option:</span><span class="sxs-lookup"><span data-stu-id="51b46-142">To see a list of options for `account` commands, use the `-help` option:</span></span>

    azure account -help

<span data-ttu-id="51b46-143">After importing your publish settings, you should delete the `.publishsettings` file for security reasons.</span><span class="sxs-lookup"><span data-stu-id="51b46-143">After importing your publish settings, you should delete the `.publishsettings` file for security reasons.</span></span>

> [!NOTE]
> <span data-ttu-id="51b46-144">When you import publish settings, credentials for accessing your Azure subscription are stored inside your `user` folder.</span><span class="sxs-lookup"><span data-stu-id="51b46-144">When you import publish settings, credentials for accessing your Azure subscription are stored inside your `user` folder.</span></span> <span data-ttu-id="51b46-145">Your `user` folder is protected by your operating system.</span><span class="sxs-lookup"><span data-stu-id="51b46-145">Your `user` folder is protected by your operating system.</span></span> <span data-ttu-id="51b46-146">However, it is recommended that you take additional steps to encrypt your `user` folder.</span><span class="sxs-lookup"><span data-stu-id="51b46-146">However, it is recommended that you take additional steps to encrypt your `user` folder.</span></span> <span data-ttu-id="51b46-147">You can do so in the following ways:</span><span class="sxs-lookup"><span data-stu-id="51b46-147">You can do so in the following ways:</span></span>    
> 
> * <span data-ttu-id="51b46-148">On Windows, modify the folder properties or use BitLocker.</span><span class="sxs-lookup"><span data-stu-id="51b46-148">On Windows, modify the folder properties or use BitLocker.</span></span>
> * <span data-ttu-id="51b46-149">On Mac, turn on FileVault for the folder.</span><span class="sxs-lookup"><span data-stu-id="51b46-149">On Mac, turn on FileVault for the folder.</span></span>
> * <span data-ttu-id="51b46-150">On Ubuntu, use the Encrypted Home directory feature.</span><span class="sxs-lookup"><span data-stu-id="51b46-150">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="51b46-151">Other Linux distributions offer equivalent features.</span><span class="sxs-lookup"><span data-stu-id="51b46-151">Other Linux distributions offer equivalent features.</span></span>
> 
> 

<span data-ttu-id="51b46-152">You are now ready to being creating and managing Azure Websites and Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="51b46-152">You are now ready to being creating and managing Azure Websites and Azure Virtual Machines.</span></span>  

<h2><a id="WebSites"></a><span data-ttu-id="51b46-153">How to create and manage an Azure Website</span><span class="sxs-lookup"><span data-stu-id="51b46-153">How to create and manage an Azure Website</span></span></h2>

### <a name="create-a-website"></a><span data-ttu-id="51b46-154">Create a Website</span><span class="sxs-lookup"><span data-stu-id="51b46-154">Create a Website</span></span>
<span data-ttu-id="51b46-155">To create an Azure website, first create an empty directory called `MySite` and browse into that directory.</span><span class="sxs-lookup"><span data-stu-id="51b46-155">To create an Azure website, first create an empty directory called `MySite` and browse into that directory.</span></span>

<span data-ttu-id="51b46-156">Then, run the following command:</span><span class="sxs-lookup"><span data-stu-id="51b46-156">Then, run the following command:</span></span>

    azure site create MySite --git

<span data-ttu-id="51b46-157">The output from this command will contain the default URL for the newly created website.</span><span class="sxs-lookup"><span data-stu-id="51b46-157">The output from this command will contain the default URL for the newly created website.</span></span> <span data-ttu-id="51b46-158">The `--git` option allows you to use git to publish to your website by creating git repositories in both your local application directory and in your website's data center.</span><span class="sxs-lookup"><span data-stu-id="51b46-158">The `--git` option allows you to use git to publish to your website by creating git repositories in both your local application directory and in your website's data center.</span></span> <span data-ttu-id="51b46-159">Note that if your local folder is already a git repository, the command will add a new remote to the existing repository, pointing to the repository in your website's data center.</span><span class="sxs-lookup"><span data-stu-id="51b46-159">Note that if your local folder is already a git repository, the command will add a new remote to the existing repository, pointing to the repository in your website's data center.</span></span>

<span data-ttu-id="51b46-160">Note that you can execute the `azure site create` command with any of the following options:</span><span class="sxs-lookup"><span data-stu-id="51b46-160">Note that you can execute the `azure site create` command with any of the following options:</span></span>

* <span data-ttu-id="51b46-161">`--location [location name]`.</span><span class="sxs-lookup"><span data-stu-id="51b46-161">`--location [location name]`.</span></span> <span data-ttu-id="51b46-162">This option allows you to specify the location of the data center in which your website is created (e.g. "West US").</span><span class="sxs-lookup"><span data-stu-id="51b46-162">This option allows you to specify the location of the data center in which your website is created (e.g. "West US").</span></span> <span data-ttu-id="51b46-163">If you omit this option, you will be promted to choose a location.</span><span class="sxs-lookup"><span data-stu-id="51b46-163">If you omit this option, you will be promted to choose a location.</span></span>
* <span data-ttu-id="51b46-164">`--hostname [custom host name]`.</span><span class="sxs-lookup"><span data-stu-id="51b46-164">`--hostname [custom host name]`.</span></span> <span data-ttu-id="51b46-165">This option allows you to specify a custom hostname for your website.</span><span class="sxs-lookup"><span data-stu-id="51b46-165">This option allows you to specify a custom hostname for your website.</span></span>

<span data-ttu-id="51b46-166">You can then add content to your website directory.</span><span class="sxs-lookup"><span data-stu-id="51b46-166">You can then add content to your website directory.</span></span> <span data-ttu-id="51b46-167">Use the regular git flow (`git add`, `git commit`) to commit your content.</span><span class="sxs-lookup"><span data-stu-id="51b46-167">Use the regular git flow (`git add`, `git commit`) to commit your content.</span></span> <span data-ttu-id="51b46-168">Use the following git command to push your website content to Azure:</span><span class="sxs-lookup"><span data-stu-id="51b46-168">Use the following git command to push your website content to Azure:</span></span> 

    git push azure master

### <a name="set-up-publishing-from-github"></a><span data-ttu-id="51b46-169">Set up publishing from GitHub</span><span class="sxs-lookup"><span data-stu-id="51b46-169">Set up publishing from GitHub</span></span>
<span data-ttu-id="51b46-170">To set up continuous publishing from a GitHub repository, use the `--GitHub` option when creating a site:</span><span class="sxs-lookup"><span data-stu-id="51b46-170">To set up continuous publishing from a GitHub repository, use the `--GitHub` option when creating a site:</span></span>

    auzre site create MySite --github --githubusername username --githubpassword password --githubrepository githubuser/reponame

<span data-ttu-id="51b46-171">If you have a local clone of a GitHub repository or if you have a repository with a single remote reference to a GitHub repository, this command will automatically publish code in the GitHub repository to your site.</span><span class="sxs-lookup"><span data-stu-id="51b46-171">If you have a local clone of a GitHub repository or if you have a repository with a single remote reference to a GitHub repository, this command will automatically publish code in the GitHub repository to your site.</span></span> <span data-ttu-id="51b46-172">From then on, any changes pushed to the GitHub repository will automatically be published to your site.</span><span class="sxs-lookup"><span data-stu-id="51b46-172">From then on, any changes pushed to the GitHub repository will automatically be published to your site.</span></span>

<span data-ttu-id="51b46-173">When you set up publishing from GitHub, the default branch used is the master branch.</span><span class="sxs-lookup"><span data-stu-id="51b46-173">When you set up publishing from GitHub, the default branch used is the master branch.</span></span> <span data-ttu-id="51b46-174">To specify a different branch, execute the following command from your local repository:</span><span class="sxs-lookup"><span data-stu-id="51b46-174">To specify a different branch, execute the following command from your local repository:</span></span>

    azure site repository <branch name>

### <a name="configure-app-settings"></a><span data-ttu-id="51b46-175">Configure app settings</span><span class="sxs-lookup"><span data-stu-id="51b46-175">Configure app settings</span></span>
<span data-ttu-id="51b46-176">App settings are key-value pairs that are available to your application at runtime.</span><span class="sxs-lookup"><span data-stu-id="51b46-176">App settings are key-value pairs that are available to your application at runtime.</span></span> <span data-ttu-id="51b46-177">When set for an Azure Website, app setting values will override settings with the same key that are defined in your site's Web.config file.</span><span class="sxs-lookup"><span data-stu-id="51b46-177">When set for an Azure Website, app setting values will override settings with the same key that are defined in your site's Web.config file.</span></span> <span data-ttu-id="51b46-178">For Node.js and PHP applications, app settings are available as environment variables.</span><span class="sxs-lookup"><span data-stu-id="51b46-178">For Node.js and PHP applications, app settings are available as environment variables.</span></span> <span data-ttu-id="51b46-179">The following example shows you how to set a key-value pair:</span><span class="sxs-lookup"><span data-stu-id="51b46-179">The following example shows you how to set a key-value pair:</span></span>

    azure site config add <key>=<value> 

<span data-ttu-id="51b46-180">To see a list of all key/value pairs, use the following:</span><span class="sxs-lookup"><span data-stu-id="51b46-180">To see a list of all key/value pairs, use the following:</span></span>

    azure site config list 

<span data-ttu-id="51b46-181">Or if you know the key and want to see the value, you can use:</span><span class="sxs-lookup"><span data-stu-id="51b46-181">Or if you know the key and want to see the value, you can use:</span></span>

    azure site config get <key> 

<span data-ttu-id="51b46-182">If you want to change the value of an existing key you must first clear the existing key and then re-add it.</span><span class="sxs-lookup"><span data-stu-id="51b46-182">If you want to change the value of an existing key you must first clear the existing key and then re-add it.</span></span> <span data-ttu-id="51b46-183">The clear command is:</span><span class="sxs-lookup"><span data-stu-id="51b46-183">The clear command is:</span></span>

    azure site config clear <key> 

### <a name="list-and-show-sites"></a><span data-ttu-id="51b46-184">List and show sites</span><span class="sxs-lookup"><span data-stu-id="51b46-184">List and show sites</span></span>
<span data-ttu-id="51b46-185">To list your websites, use the following command:</span><span class="sxs-lookup"><span data-stu-id="51b46-185">To list your websites, use the following command:</span></span>

    azure site list

<span data-ttu-id="51b46-186">To get detailed information about a site, use the `site show` command.</span><span class="sxs-lookup"><span data-stu-id="51b46-186">To get detailed information about a site, use the `site show` command.</span></span> <span data-ttu-id="51b46-187">The following example shows details for `MySite`:</span><span class="sxs-lookup"><span data-stu-id="51b46-187">The following example shows details for `MySite`:</span></span>

    azure site show MySite

### <a name="stop-start-or-restart-a-site"></a><span data-ttu-id="51b46-188">Stop, start, or restart a site</span><span class="sxs-lookup"><span data-stu-id="51b46-188">Stop, start, or restart a site</span></span>
<span data-ttu-id="51b46-189">You can stop, start, or restart a site with the `site stop`, `site start`, or `site restart` commands:</span><span class="sxs-lookup"><span data-stu-id="51b46-189">You can stop, start, or restart a site with the `site stop`, `site start`, or `site restart` commands:</span></span>

    azure site stop MySite
    azure site start MySite
    azure site restart MySite

### <a name="delete-a-site"></a><span data-ttu-id="51b46-190">Delete a site</span><span class="sxs-lookup"><span data-stu-id="51b46-190">Delete a site</span></span>
<span data-ttu-id="51b46-191">Finally, you can delete a site with the `site delete` command:</span><span class="sxs-lookup"><span data-stu-id="51b46-191">Finally, you can delete a site with the `site delete` command:</span></span>

    azure site delete MySite

<span data-ttu-id="51b46-192">Note that if you are running any of above commands from inside the folder where you ran `site create`, you do not need to specify the site name `MySite` as the last parameter.</span><span class="sxs-lookup"><span data-stu-id="51b46-192">Note that if you are running any of above commands from inside the folder where you ran `site create`, you do not need to specify the site name `MySite` as the last parameter.</span></span>

<span data-ttu-id="51b46-193">To see a complete list of `site` commands, use the `-help` option:</span><span class="sxs-lookup"><span data-stu-id="51b46-193">To see a complete list of `site` commands, use the `-help` option:</span></span>

    azure site -help 

<h2><a id="VMs"></a><span data-ttu-id="51b46-194">How to create and manage an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="51b46-194">How to create and manage an Azure Virtual Machine</span></span></h2>

<span data-ttu-id="51b46-195">an Azure Virtual Machine is created from a virtual machine image (a .vhd file) that you provide or that is available in the Image Gallery.</span><span class="sxs-lookup"><span data-stu-id="51b46-195">an Azure Virtual Machine is created from a virtual machine image (a .vhd file) that you provide or that is available in the Image Gallery.</span></span> <span data-ttu-id="51b46-196">To see images that are available, use the `vm image list` command:</span><span class="sxs-lookup"><span data-stu-id="51b46-196">To see images that are available, use the `vm image list` command:</span></span>

    azure vm image list

<span data-ttu-id="51b46-197">You can provision and start a virtual machine from one of the available images with the `vm create` command.</span><span class="sxs-lookup"><span data-stu-id="51b46-197">You can provision and start a virtual machine from one of the available images with the `vm create` command.</span></span> <span data-ttu-id="51b46-198">The following example shows how to create a Linux virtual machine (called `myVM`) from an image in the Image Gallery (CentOS 6.2).</span><span class="sxs-lookup"><span data-stu-id="51b46-198">The following example shows how to create a Linux virtual machine (called `myVM`) from an image in the Image Gallery (CentOS 6.2).</span></span> <span data-ttu-id="51b46-199">The root user name and password for the virtual machine are `myusername` and `Mypassw0rd` respectively.</span><span class="sxs-lookup"><span data-stu-id="51b46-199">The root user name and password for the virtual machine are `myusername` and `Mypassw0rd` respectively.</span></span> <span data-ttu-id="51b46-200">(Note that the `--location` parameter specifies the data center in which the virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="51b46-200">(Note that the `--location` parameter specifies the data center in which the virtual machine is created.</span></span> <span data-ttu-id="51b46-201">If you omit the `--location` parameter, you will be prompted to choose a location.)</span><span class="sxs-lookup"><span data-stu-id="51b46-201">If you omit the `--location` parameter, you will be prompted to choose a location.)</span></span>

    azure vm create myVM OpenLogic__OpenLogic-CentOS-62-20120509-en-us-30GB.vhd myusername --location "West US"

<span data-ttu-id="51b46-202">You may consider passing the `--ssh` flag (Linux) or `--rdp` flag (Windows) to `vm create` to enable remote connections to the newly-created virtual machine.</span><span class="sxs-lookup"><span data-stu-id="51b46-202">You may consider passing the `--ssh` flag (Linux) or `--rdp` flag (Windows) to `vm create` to enable remote connections to the newly-created virtual machine.</span></span>

<span data-ttu-id="51b46-203">If you would rather provision a virtual machine from a custom image, you can create an image from a .vhd file with the `vm image create` command, then use the `vm create` command to provision the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="51b46-203">If you would rather provision a virtual machine from a custom image, you can create an image from a .vhd file with the `vm image create` command, then use the `vm create` command to provision the virtual machine.</span></span> <span data-ttu-id="51b46-204">The following example shows how to create a Linux image (called `myImage`) from a local .vhd file.</span><span class="sxs-lookup"><span data-stu-id="51b46-204">The following example shows how to create a Linux image (called `myImage`) from a local .vhd file.</span></span> <span data-ttu-id="51b46-205">(The `--location` parameter specifies the data in which the image is stored.)</span><span class="sxs-lookup"><span data-stu-id="51b46-205">(The `--location` parameter specifies the data in which the image is stored.)</span></span>

    azure vm image create myImage /path/to/myImage.vhd --os linux --location "West US"

<span data-ttu-id="51b46-206">Instead of creating an image from a local .vhd, you can create an image from a .vhd stored in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="51b46-206">Instead of creating an image from a local .vhd, you can create an image from a .vhd stored in Azure Blob Storage.</span></span> <span data-ttu-id="51b46-207">You can do this with the `blob-url` parameter:</span><span class="sxs-lookup"><span data-stu-id="51b46-207">You can do this with the `blob-url` parameter:</span></span>

    azure vm image create myImage --blob-url <url to .vhd in Blob Storage> --os linux

<span data-ttu-id="51b46-208">After creating an image, you can provision a virtual machine from the image by using `vm create`.</span><span class="sxs-lookup"><span data-stu-id="51b46-208">After creating an image, you can provision a virtual machine from the image by using `vm create`.</span></span> <span data-ttu-id="51b46-209">The command below creates a virtual machine called `myVM` from the image created above (`myImage`).</span><span class="sxs-lookup"><span data-stu-id="51b46-209">The command below creates a virtual machine called `myVM` from the image created above (`myImage`).</span></span>

    azure vm create myVM myImage myusername --location "West US"

<span data-ttu-id="51b46-210">After you have provisioned a virtual machine, you may want to create endpoints to allow remote access to your virtual machine (for example).</span><span class="sxs-lookup"><span data-stu-id="51b46-210">After you have provisioned a virtual machine, you may want to create endpoints to allow remote access to your virtual machine (for example).</span></span> <span data-ttu-id="51b46-211">The following example uses the `vm create endpoint` command to open external port 22 and local port 22 on `myVM`:</span><span class="sxs-lookup"><span data-stu-id="51b46-211">The following example uses the `vm create endpoint` command to open external port 22 and local port 22 on `myVM`:</span></span>

    azure vm endpoint create myVM 22 22

<span data-ttu-id="51b46-212">You can get detailed information about a virtual machine (including IP address, DNS name, and endpoint information) with the `vm show` command:</span><span class="sxs-lookup"><span data-stu-id="51b46-212">You can get detailed information about a virtual machine (including IP address, DNS name, and endpoint information) with the `vm show` command:</span></span>

    azure vm show myVM

<span data-ttu-id="51b46-213">To shutdown, start, or restart the virtual machine, use one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="51b46-213">To shutdown, start, or restart the virtual machine, use one of the following commands:</span></span>

    azure vm shutdown myVM
    azure vm start myVM
    azure vm restart myVM

<span data-ttu-id="51b46-214">And finally, to delete the VM, use the `vm delete` command:</span><span class="sxs-lookup"><span data-stu-id="51b46-214">And finally, to delete the VM, use the `vm delete` command:</span></span>

    azure vm delete myVM

<span data-ttu-id="51b46-215">For a complete list of commands for creating and managing virtual machines, use the `-h` option:</span><span class="sxs-lookup"><span data-stu-id="51b46-215">For a complete list of commands for creating and managing virtual machines, use the `-h` option:</span></span>

    azure vm -h

<!-- IMAGES -->
[Azure Web Site]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/crossplat-cmd-tools/freetrial.PNG

<!-- LINKS -->
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[windows-installer]: http://go.microsoft.com/fwlink/?LinkID=275464
[reference-docs]: http://go.microsoft.com/fwlink/?LinkId=252246
[windowsazuredotcom]: http://www.windowsazure.com


