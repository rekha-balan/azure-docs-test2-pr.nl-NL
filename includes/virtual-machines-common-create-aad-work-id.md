
<br>

> [!NOTE]
> <span data-ttu-id="8ce57-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span><span class="sxs-lookup"><span data-stu-id="8ce57-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="8ce57-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span><span class="sxs-lookup"><span data-stu-id="8ce57-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="8ce57-103">If you find that you cannot use those resources, you may need to return to this article for help.</span><span class="sxs-lookup"><span data-stu-id="8ce57-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="8ce57-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="8ce57-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="8ce57-105">The steps are simple.</span><span class="sxs-lookup"><span data-stu-id="8ce57-105">The steps are simple.</span></span> <span data-ttu-id="8ce57-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span><span class="sxs-lookup"><span data-stu-id="8ce57-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="8ce57-107">Locate your default directory in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8ce57-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="8ce57-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span><span class="sxs-lookup"><span data-stu-id="8ce57-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="8ce57-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="8ce57-111">Let's start by finding some information about your identity in Azure.</span><span class="sxs-lookup"><span data-stu-id="8ce57-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="8ce57-112">You should see something like the following in the main pane, showing that you have one default directory.</span><span class="sxs-lookup"><span data-stu-id="8ce57-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="8ce57-113">Let's find out some more information about it.</span><span class="sxs-lookup"><span data-stu-id="8ce57-113">Let's find out some more information about it.</span></span> <span data-ttu-id="8ce57-114">Click the default directory row, which brings you into the default directory properties.</span><span class="sxs-lookup"><span data-stu-id="8ce57-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="8ce57-115">To view the default domain name, click **DOMAINS**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-115">To view the default domain name, click **DOMAINS**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="8ce57-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8ce57-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="8ce57-117">That's the domain to which you will now add a new user.</span><span class="sxs-lookup"><span data-stu-id="8ce57-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="8ce57-118">Creating a new user in the default domain</span><span class="sxs-lookup"><span data-stu-id="8ce57-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="8ce57-119">Click **USERS** and look for your single personal account.</span><span class="sxs-lookup"><span data-stu-id="8ce57-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="8ce57-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="8ce57-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="8ce57-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="8ce57-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span><span class="sxs-lookup"><span data-stu-id="8ce57-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="8ce57-123">At the bottom of the page, click **+ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="8ce57-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="8ce57-125">In this example, the new user name is `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="8ce57-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="8ce57-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span><span class="sxs-lookup"><span data-stu-id="8ce57-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="8ce57-127">Click the next arrow when finished.</span><span class="sxs-lookup"><span data-stu-id="8ce57-127">Click the next arrow when finished.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="8ce57-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span><span class="sxs-lookup"><span data-stu-id="8ce57-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="8ce57-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span><span class="sxs-lookup"><span data-stu-id="8ce57-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="8ce57-130">This example uses the **User** role.</span><span class="sxs-lookup"><span data-stu-id="8ce57-130">This example uses the **User** role.</span></span> <span data-ttu-id="8ce57-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span><span class="sxs-lookup"><span data-stu-id="8ce57-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="8ce57-132">Click the next arrow when you're finished.</span><span class="sxs-lookup"><span data-stu-id="8ce57-132">Click the next arrow when you're finished.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="8ce57-133">Click the **create** button to generate and display a temporary password for Ahmet.</span><span class="sxs-lookup"><span data-stu-id="8ce57-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="8ce57-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="8ce57-135">You'll need the information to log on shortly.</span><span class="sxs-lookup"><span data-stu-id="8ce57-135">You'll need the information to log on shortly.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="8ce57-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ce57-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="8ce57-137">You've created the new work or school identity with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ce57-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="8ce57-138">However, this identity does not yet have permissions to use Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8ce57-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="8ce57-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span><span class="sxs-lookup"><span data-stu-id="8ce57-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="8ce57-140">Adding Azure co-administrator rights for subscriptions</span><span class="sxs-lookup"><span data-stu-id="8ce57-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="8ce57-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="8ce57-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="8ce57-142">To do this, in the lower-left panel click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="8ce57-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="8ce57-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span><span class="sxs-lookup"><span data-stu-id="8ce57-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="8ce57-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span><span class="sxs-lookup"><span data-stu-id="8ce57-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="8ce57-145">Here, enter the email address of the new user you had created, including your default domain.</span><span class="sxs-lookup"><span data-stu-id="8ce57-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="8ce57-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span><span class="sxs-lookup"><span data-stu-id="8ce57-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="8ce57-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span><span class="sxs-lookup"><span data-stu-id="8ce57-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="8ce57-148">When you are done, you should now see two users, including your new co-administrator identity.</span><span class="sxs-lookup"><span data-stu-id="8ce57-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="8ce57-149">Log out of the portal.</span><span class="sxs-lookup"><span data-stu-id="8ce57-149">Log out of the portal.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="8ce57-150">Logging in and changing the new user's password</span><span class="sxs-lookup"><span data-stu-id="8ce57-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="8ce57-151">Log in as the new user you created.</span><span class="sxs-lookup"><span data-stu-id="8ce57-151">Log in as the new user you created.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="8ce57-152">You will immediately be prompted to create a new password.</span><span class="sxs-lookup"><span data-stu-id="8ce57-152">You will immediately be prompted to create a new password.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="8ce57-153">You should be rewarded with success that looks like the following.</span><span class="sxs-lookup"><span data-stu-id="8ce57-153">You should be rewarded with success that looks like the following.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="8ce57-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ce57-154">Next steps</span></span>
<span data-ttu-id="8ce57-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ce57-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK

















