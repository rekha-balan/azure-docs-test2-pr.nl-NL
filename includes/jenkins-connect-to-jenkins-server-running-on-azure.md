1. <span data-ttu-id="fb1d9-101">In your browser, navigate to your Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-101">In your browser, navigate to your Jenkins virtual machine.</span></span> <span data-ttu-id="fb1d9-102">Since the Jenkins dashboard is inaccessible through unsecured HTTP, a message displays indicating that you need to use SSH to tunnel into the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-102">Since the Jenkins dashboard is inaccessible through unsecured HTTP, a message displays indicating that you need to use SSH to tunnel into the virtual machine.</span></span>

    ![Jenkins provides information explaining how to use SSH to connect to the Jenkins virtual machine.](./media/jenkins-connect-to-jenkins-server-running-on-azure/jenkins-ssh-instructions.png)

1. <span data-ttu-id="fb1d9-104">Open a bash or terminal window, with access to SSH.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-104">Open a bash or terminal window, with access to SSH.</span></span>

1. <span data-ttu-id="fb1d9-105">Enter the following `ssh` command, replacing the **&lt;username>** and **&lt;domain>** placeholders with the values specified when creating the Jenkins virtual machine:</span><span class="sxs-lookup"><span data-stu-id="fb1d9-105">Enter the following `ssh` command, replacing the **&lt;username>** and **&lt;domain>** placeholders with the values specified when creating the Jenkins virtual machine:</span></span>

    ```bash
    ssh -L 127.0.0.1:8080:localhost:8080 <username>@<domain>.eastus.cloudapp.azure.com
    ```

1. <span data-ttu-id="fb1d9-106">Follow the `ssh` prompts to sign in to the Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-106">Follow the `ssh` prompts to sign in to the Jenkins virtual machine.</span></span>

1. <span data-ttu-id="fb1d9-107">Enter the following command to retrieve the initial password for unlocking Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-107">Enter the following command to retrieve the initial password for unlocking Jenkins.</span></span>

    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```

1. <span data-ttu-id="fb1d9-108">Copy to the clipboard the password that is displayed in the bash or terminal window.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-108">Copy to the clipboard the password that is displayed in the bash or terminal window.</span></span>

1. <span data-ttu-id="fb1d9-109">In your browser, navigate to `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-109">In your browser, navigate to `http://localhost:8080`.</span></span>

1. <span data-ttu-id="fb1d9-110">Paste the password retrieved earlier into the **Administrative password** field, and select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-110">Paste the password retrieved earlier into the **Administrative password** field, and select **Continue**.</span></span>

    ![Jenkins stores an initial password that you must use to unlock the Jenkins virtual machine the first time you connect to it.](./media/jenkins-connect-to-jenkins-server-running-on-azure/jenkins-unlock.png)

1. <span data-ttu-id="fb1d9-112">Select **Install suggested plugins**.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-112">Select **Install suggested plugins**.</span></span>

    ![Jenkins allows you to easily install a collection of suggested plugins upon initial entry](./media/jenkins-connect-to-jenkins-server-running-on-azure/jenkins-customize.png)

1. <span data-ttu-id="fb1d9-114">On the **Create First Admin User** page, create the administrative user and password for the Jenkins dashboard, and select **Save and finish**.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-114">On the **Create First Admin User** page, create the administrative user and password for the Jenkins dashboard, and select **Save and finish**.</span></span>

1. <span data-ttu-id="fb1d9-115">On the **Jenkins is ready!**</span><span class="sxs-lookup"><span data-stu-id="fb1d9-115">On the **Jenkins is ready!**</span></span> <span data-ttu-id="fb1d9-116">page, select **Start using Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="fb1d9-116">page, select **Start using Jenkins**.</span></span>

    ![Once Jenkins is installed and configured for access, you can start using it to create and build jobs.](./media/jenkins-connect-to-jenkins-server-running-on-azure/jenkins-ready.png)