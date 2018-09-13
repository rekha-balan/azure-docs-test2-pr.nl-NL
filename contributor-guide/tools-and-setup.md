# <a name="install-and-set-up-tools-for-authoring-in-github"></a><span data-ttu-id="f5fb1-101">Install and set up tools for authoring in GitHub</span><span class="sxs-lookup"><span data-stu-id="f5fb1-101">Install and set up tools for authoring in GitHub</span></span>

<span data-ttu-id="f5fb1-102">Follow the steps in this article to set up tools for contributing to the Azure technical documentation.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-102">Follow the steps in this article to set up tools for contributing to the Azure technical documentation.</span></span> <span data-ttu-id="f5fb1-103">Casual and occasional contributors probably can use the GitHub UI described in step 2.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-103">Casual and occasional contributors probably can use the GitHub UI described in step 2.</span></span>

<span data-ttu-id="f5fb1-104">If you're unfamiliar with Git, you might want to review some Git terminology: [https://help.github.com/articles/github-glossary](https://help.github.com/articles/github-glossary).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-104">If you're unfamiliar with Git, you might want to review some Git terminology: [https://help.github.com/articles/github-glossary](https://help.github.com/articles/github-glossary).</span></span> <span data-ttu-id="f5fb1-105">In addition, this StackOverflow thread contains a glossary of Git terms you'll encounter here: [http://stackoverflow.com/questions/7076164/terminology-used-by-git](http://stackoverflow.com/questions/7076164/terminology-used-by-git)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-105">In addition, this StackOverflow thread contains a glossary of Git terms you'll encounter here: [http://stackoverflow.com/questions/7076164/terminology-used-by-git](http://stackoverflow.com/questions/7076164/terminology-used-by-git)</span></span>

## <a name="contents"></a><span data-ttu-id="f5fb1-106">Contents</span><span class="sxs-lookup"><span data-stu-id="f5fb1-106">Contents</span></span>
* [<span data-ttu-id="f5fb1-107">Create a GitHub account and set up your profile</span><span class="sxs-lookup"><span data-stu-id="f5fb1-107">Create a GitHub account and set up your profile</span></span>](#create-a-github-account-and-set-up-your-profile)
* [<span data-ttu-id="f5fb1-108">Sign up for LiveFyre</span><span class="sxs-lookup"><span data-stu-id="f5fb1-108">Sign up for LiveFyre</span></span>](#sign-up-for-livefyre)
* [<span data-ttu-id="f5fb1-109">Modify articles using the GitHub UI</span><span class="sxs-lookup"><span data-stu-id="f5fb1-109">Modify articles using the GitHub UI</span></span>](#modify-articles-using-the-github-ui)
* [<span data-ttu-id="f5fb1-110">Private or public repo?</span><span class="sxs-lookup"><span data-stu-id="f5fb1-110">Private or public repo?</span></span>](#private-or-public-repo?)
* [<span data-ttu-id="f5fb1-111">Permissions</span><span class="sxs-lookup"><span data-stu-id="f5fb1-111">Permissions</span></span>](#permissions)
* [<span data-ttu-id="f5fb1-112">Install Git for Windows</span><span class="sxs-lookup"><span data-stu-id="f5fb1-112">Install Git for Windows</span></span>](#install-git-for-windows)
* [<span data-ttu-id="f5fb1-113">Enable two-factor authentication</span><span class="sxs-lookup"><span data-stu-id="f5fb1-113">Enable two-factor authentication</span></span>](#enable-two-factor-authentication)
* [<span data-ttu-id="f5fb1-114">Install a markdown editor</span><span class="sxs-lookup"><span data-stu-id="f5fb1-114">Install a markdown editor</span></span>](#install-a-markdown-editor)
* [<span data-ttu-id="f5fb1-115">Configure Atom</span><span class="sxs-lookup"><span data-stu-id="f5fb1-115">Configure Atom</span></span>](#configure-atom)
* [<span data-ttu-id="f5fb1-116">Fork the repository and copy it to your computer</span><span class="sxs-lookup"><span data-stu-id="f5fb1-116">Fork the repository and copy it to your computer</span></span>](#fork-the-repository-and-copy-it-to-your-computer)
* [<span data-ttu-id="f5fb1-117">Configure your user name and email locally</span><span class="sxs-lookup"><span data-stu-id="f5fb1-117">Configure your user name and email locally</span></span>](#configure-your-user-name-and-email-locally)
* [<span data-ttu-id="f5fb1-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5fb1-118">Next steps</span></span>](#next-steps)

## <a name="create-a-github-account-and-set-up-your-profile"></a><span data-ttu-id="f5fb1-119">Create a GitHub account and set up your profile</span><span class="sxs-lookup"><span data-stu-id="f5fb1-119">Create a GitHub account and set up your profile</span></span>
<span data-ttu-id="f5fb1-120">To contribute to the Azure technical content, you'll need a [GitHub](http://www.github.com) account.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-120">To contribute to the Azure technical content, you'll need a [GitHub](http://www.github.com) account.</span></span> <span data-ttu-id="f5fb1-121">If you are a Microsoft contributor, you need to set up your GitHub account so you're clearly identified as a Microsoft employee.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-121">If you are a Microsoft contributor, you need to set up your GitHub account so you're clearly identified as a Microsoft employee.</span></span> <span data-ttu-id="f5fb1-122">Set up your profile as follows:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-122">Set up your profile as follows:</span></span>

* <span data-ttu-id="f5fb1-123">**Profile picture**: a picture of you (required)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-123">**Profile picture**: a picture of you (required)</span></span>
* <span data-ttu-id="f5fb1-124">**Name**: your first and last name (required)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-124">**Name**: your first and last name (required)</span></span>
* <span data-ttu-id="f5fb1-125">**Email**: your Microsoft email address (optional)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-125">**Email**: your Microsoft email address (optional)</span></span>
* <span data-ttu-id="f5fb1-126">**Company**: Microsoft Corporation (required)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-126">**Company**: Microsoft Corporation (required)</span></span>
* <span data-ttu-id="f5fb1-127">**Location**: list your location (optional)</span><span class="sxs-lookup"><span data-stu-id="f5fb1-127">**Location**: list your location (optional)</span></span>

<span data-ttu-id="f5fb1-128">Your profile should resemble this profile:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-128">Your profile should resemble this profile:</span></span>

<p align="center">
 ![GitHub profile example](./media/tools-and-setup/githubprofile.png)

## <a name="sign-up-for-livefyre"></a><span data-ttu-id="f5fb1-130">Sign up for Livefyre</span><span class="sxs-lookup"><span data-stu-id="f5fb1-130">Sign up for Livefyre</span></span>

<span data-ttu-id="f5fb1-131">Every published technical article supports a comment stream provided by the [Livefyre](http://web.livefyre.com/) service.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-131">Every published technical article supports a comment stream provided by the [Livefyre](http://web.livefyre.com/) service.</span></span> 

<span data-ttu-id="f5fb1-132">As a Microsoft employee and article author or contributor, you need to sign up for Livefyre so you can participate in the comment stream for the article.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-132">As a Microsoft employee and article author or contributor, you need to sign up for Livefyre so you can participate in the comment stream for the article.</span></span> 

1. <span data-ttu-id="f5fb1-133">Your Livefyre account needs to be created within docs.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-133">Your Livefyre account needs to be created within docs.microsoft.com.</span></span> <span data-ttu-id="f5fb1-134">Pick an article in docs.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-134">Pick an article in docs.microsoft.com.</span></span> <span data-ttu-id="f5fb1-135">E.g.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-135">E.g.</span></span>  <span data-ttu-id="f5fb1-136">[https://docs.microsoft.com/en-us/active-directory/active-directory-developers-guide](https://docs.microsoft.com/en-us/active-directory/active-directory-developers-guide).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-136">[https://docs.microsoft.com/en-us/active-directory/active-directory-developers-guide](https://docs.microsoft.com/en-us/active-directory/active-directory-developers-guide).</span></span>

2. <span data-ttu-id="f5fb1-137">At the bottom of the article, click the *Sign in* link in the comments section.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-137">At the bottom of the article, click the *Sign in* link in the comments section.</span></span>
 
3. <span data-ttu-id="f5fb1-138">In the authentication dialog, click *Create New Account*.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-138">In the authentication dialog, click *Create New Account*.</span></span>
  
4. <span data-ttu-id="f5fb1-139">Enter your profile information and click *Sign up*.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-139">Enter your profile information and click *Sign up*.</span></span>
   - <span data-ttu-id="f5fb1-140">**Username**: your Microsoft email alias plus @MSFT, ie: *alias@MSFT*</span><span class="sxs-lookup"><span data-stu-id="f5fb1-140">**Username**: your Microsoft email alias plus @MSFT, ie: *alias@MSFT*</span></span>
   - <span data-ttu-id="f5fb1-141">**Email**: Your Microsoft.com email address.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-141">**Email**: Your Microsoft.com email address.</span></span>
  
## <a name="modify-articles-using-the-github-ui"></a><span data-ttu-id="f5fb1-142">Modify articles using the GitHub UI</span><span class="sxs-lookup"><span data-stu-id="f5fb1-142">Modify articles using the GitHub UI</span></span>
<span data-ttu-id="f5fb1-143">You might not need to follow all the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-143">You might not need to follow all the steps in this article.</span></span> <span data-ttu-id="f5fb1-144">It depends on the sort of content contribution you want or need to make.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-144">It depends on the sort of content contribution you want or need to make.</span></span>

### <a name="submit-a-text-only-change-to-an-existing-article"></a><span data-ttu-id="f5fb1-145">Submit a text-only change to an existing article</span><span class="sxs-lookup"><span data-stu-id="f5fb1-145">Submit a text-only change to an existing article</span></span>
<span data-ttu-id="f5fb1-146">If you only need or want to make textual updates to an existing article, you probably don't need to follow the rest of the steps.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-146">If you only need or want to make textual updates to an existing article, you probably don't need to follow the rest of the steps.</span></span> <span data-ttu-id="f5fb1-147">You can use GitHub's web-based markdown editor to submit your changes.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-147">You can use GitHub's web-based markdown editor to submit your changes.</span></span> 

1. <span data-ttu-id="f5fb1-148">Click the Edit button on the article page you want to modify.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-148">Click the Edit button on the article page you want to modify.</span></span>

2. <span data-ttu-id="f5fb1-149">Then, click the edit icon in the GitHub version of the article</span><span class="sxs-lookup"><span data-stu-id="f5fb1-149">Then, click the edit icon in the GitHub version of the article</span></span>

 ![GitHub profile example](./media/tools-and-setup/editicon.PNG)

 <span data-ttu-id="f5fb1-151">That opens the easy-to-use web editor that makes it easy to submit changes.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-151">That opens the easy-to-use web editor that makes it easy to submit changes.</span></span> <span data-ttu-id="f5fb1-152">You don't need to follow the other steps in this article.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-152">You don't need to follow the other steps in this article.</span></span>

### <a name="all-other-changes"></a><span data-ttu-id="f5fb1-153">All other changes</span><span class="sxs-lookup"><span data-stu-id="f5fb1-153">All other changes</span></span>
<span data-ttu-id="f5fb1-154">The GitHub UI does support creation of new files and dragging and dropping images.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-154">The GitHub UI does support creation of new files and dragging and dropping images.</span></span> <span data-ttu-id="f5fb1-155">However, when you work in the UI, managing branches can be confusing so we typically recommend you install the tools and learn the commands for creating and managing articles.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-155">However, when you work in the UI, managing branches can be confusing so we typically recommend you install the tools and learn the commands for creating and managing articles.</span></span> <span data-ttu-id="f5fb1-156">If you want to use the UI, see:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-156">If you want to use the UI, see:</span></span>

* [<span data-ttu-id="f5fb1-157">Creating files on GitHub</span><span class="sxs-lookup"><span data-stu-id="f5fb1-157">Creating files on GitHub</span></span>](https://github.com/blog/1327-creating-files-on-github)
* [<span data-ttu-id="f5fb1-158">Upload files to your repositories</span><span class="sxs-lookup"><span data-stu-id="f5fb1-158">Upload files to your repositories</span></span>](https://github.com/blog/2105-upload-files-to-your-repositories)

<span data-ttu-id="f5fb1-159">For the following sorts of work, we strongly recommend you install and learn to use the tools:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-159">For the following sorts of work, we strongly recommend you install and learn to use the tools:</span></span>

* <span data-ttu-id="f5fb1-160">Making major changes to an article</span><span class="sxs-lookup"><span data-stu-id="f5fb1-160">Making major changes to an article</span></span>
* <span data-ttu-id="f5fb1-161">Creating and publishing a new article</span><span class="sxs-lookup"><span data-stu-id="f5fb1-161">Creating and publishing a new article</span></span>
* <span data-ttu-id="f5fb1-162">Adding new images or updating images</span><span class="sxs-lookup"><span data-stu-id="f5fb1-162">Adding new images or updating images</span></span>
* <span data-ttu-id="f5fb1-163">Updating an article over a period of days without publishing changes each of those days</span><span class="sxs-lookup"><span data-stu-id="f5fb1-163">Updating an article over a period of days without publishing changes each of those days</span></span>
* <span data-ttu-id="f5fb1-164">Creating content for a release that has to go out on a certain day at a certain time</span><span class="sxs-lookup"><span data-stu-id="f5fb1-164">Creating content for a release that has to go out on a certain day at a certain time</span></span>

## <a name="private-or-public-repo"></a><span data-ttu-id="f5fb1-165">Private or public repo?</span><span class="sxs-lookup"><span data-stu-id="f5fb1-165">Private or public repo?</span></span>
 
 <span data-ttu-id="f5fb1-166">The public repository is for the community and for occasional internal Microsoft contrbutors who are not listed as authors of articles or responsible as owners of articles.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-166">The public repository is for the community and for occasional internal Microsoft contrbutors who are not listed as authors of articles or responsible as owners of articles.</span></span>

 <span data-ttu-id="f5fb1-167">If you are the author of an article and you are a Microsoft employee, you must work in the private repo.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-167">If you are the author of an article and you are a Microsoft employee, you must work in the private repo.</span></span> <span data-ttu-id="f5fb1-168">Your public repo contributions will be automatically closed by our repo automation.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-168">Your public repo contributions will be automatically closed by our repo automation.</span></span> <span data-ttu-id="f5fb1-169">Request permissions to the private repo, per the instructions in the next section.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-169">Request permissions to the private repo, per the instructions in the next section.</span></span>
 
 <span data-ttu-id="f5fb1-170">To easily switch from the public repo version of an article to the private repo version, just add "-pr" the URL, as shown here:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-170">To easily switch from the public repo version of an article to the private repo version, just add "-pr" the URL, as shown here:</span></span>

 - <span data-ttu-id="f5fb1-171">github.com/Microsoft/azure-docs/blob/master/articles/batch/batch-account-create-portal.md</span><span class="sxs-lookup"><span data-stu-id="f5fb1-171">github.com/Microsoft/azure-docs/blob/master/articles/batch/batch-account-create-portal.md</span></span>

 - <span data-ttu-id="f5fb1-172">github.com/Microsoft/azure-docs **-pr**/blob/master/articles/batch/batch-account-create-portal.md</span><span class="sxs-lookup"><span data-stu-id="f5fb1-172">github.com/Microsoft/azure-docs **-pr**/blob/master/articles/batch/batch-account-create-portal.md</span></span>

## <a name="permissions"></a><span data-ttu-id="f5fb1-173">Permissions</span><span class="sxs-lookup"><span data-stu-id="f5fb1-173">Permissions</span></span>
<span data-ttu-id="f5fb1-174">Anybody with a GitHub account can contribute to Azure technical content through our public repository at [https://github.com/Microsoft/azure-docs](https://github.com/Microsoft/azure-docs). No special permissions are required.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-174">Anybody with a GitHub account can contribute to Azure technical content through our public repository at [https://github.com/Microsoft/azure-docs](https://github.com/Microsoft/azure-docs). No special permissions are required.</span></span>

<span data-ttu-id="f5fb1-175">If you are a Microsoft PM or writer who is working on Azure content as a designated author or reviewer, you must work in our private content repository, azure-docs-pr.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-175">If you are a Microsoft PM or writer who is working on Azure content as a designated author or reviewer, you must work in our private content repository, azure-docs-pr.</span></span>

1. <span data-ttu-id="f5fb1-176">Visit [https://repos.opensource.microsoft.com ](https://repos.opensource.microsoft.com) to join the Microsoft GitHub organization.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-176">Visit [https://repos.opensource.microsoft.com ](https://repos.opensource.microsoft.com) to join the Microsoft GitHub organization.</span></span> <span data-ttu-id="f5fb1-177">Once you are a member of the Microsoft organization, you can access the private azure-docs-pr repository.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-177">Once you are a member of the Microsoft organization, you can access the private azure-docs-pr repository.</span></span>

2. <span data-ttu-id="f5fb1-178">Register your GitHub account with the publishing system before you submit your first pull request.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-178">Register your GitHub account with the publishing system before you submit your first pull request.</span></span> <span data-ttu-id="f5fb1-179">To do this, visit https://op-portal-prod.azurewebsites.net/, and click "Sign in with GitHub".</span><span class="sxs-lookup"><span data-stu-id="f5fb1-179">To do this, visit https://op-portal-prod.azurewebsites.net/, and click "Sign in with GitHub".</span></span> <span data-ttu-id="f5fb1-180">The one-time sign-in is all that is needed.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-180">The one-time sign-in is all that is needed.</span></span> 

## <a name="install-git-for-windows"></a><span data-ttu-id="f5fb1-181">Install Git for Windows</span><span class="sxs-lookup"><span data-stu-id="f5fb1-181">Install Git for Windows</span></span>
<span data-ttu-id="f5fb1-182">Install Git for Windows from [http://git-scm.com/download/win](http://git-scm.com/download/win).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-182">Install Git for Windows from [http://git-scm.com/download/win](http://git-scm.com/download/win).</span></span> <span data-ttu-id="f5fb1-183">This download installs the Git version control system, and it installs Git Bash, the command-line app that you will use to interact with your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-183">This download installs the Git version control system, and it installs Git Bash, the command-line app that you will use to interact with your local Git repository.</span></span>

<span data-ttu-id="f5fb1-184">You can accept the default settings; if you want the commands to be available within the Windows command line, select the option that enables it.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-184">You can accept the default settings; if you want the commands to be available within the Windows command line, select the option that enables it.</span></span>

<p align="center">
 ![GitHub profile example](./media/tools-and-setup/gitbashinstall.png)

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="f5fb1-186">Enable two-factor authentication</span><span class="sxs-lookup"><span data-stu-id="f5fb1-186">Enable two-factor authentication</span></span>
<span data-ttu-id="f5fb1-187">You have to enable two factor authentication (2FA) on your GitHub account if you are working in the private content repository.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-187">You have to enable two factor authentication (2FA) on your GitHub account if you are working in the private content repository.</span></span> <span data-ttu-id="f5fb1-188">It's required.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-188">It's required.</span></span>

<span data-ttu-id="f5fb1-189">To enable 2FA, follow the instructions in both the following GitHub help topics:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-189">To enable 2FA, follow the instructions in both the following GitHub help topics:</span></span>

* [<span data-ttu-id="f5fb1-190">About Two-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f5fb1-190">About Two-Factor Authentication</span></span>](https://help.github.com/articles/about-two-factor-authentication/)
* [<span data-ttu-id="f5fb1-191">Creating an access token for command-line use</span><span class="sxs-lookup"><span data-stu-id="f5fb1-191">Creating an access token for command-line use</span></span>](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)

<span data-ttu-id="f5fb1-192">When you create the token, select all the scopes available in the token-creation UI ([details on each scope](https://developer.github.com/v3/oauth/#scopes))</span><span class="sxs-lookup"><span data-stu-id="f5fb1-192">When you create the token, select all the scopes available in the token-creation UI ([details on each scope](https://developer.github.com/v3/oauth/#scopes))</span></span>

<span data-ttu-id="f5fb1-193">After you enable 2FA, you have to enter the access token instead of your GitHub password at the command prompt when you try to access a GitHub repository from the command line.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-193">After you enable 2FA, you have to enter the access token instead of your GitHub password at the command prompt when you try to access a GitHub repository from the command line.</span></span> <span data-ttu-id="f5fb1-194">The access token is not the authentication code that you get in a text message when you set up 2FA.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-194">The access token is not the authentication code that you get in a text message when you set up 2FA.</span></span> <span data-ttu-id="f5fb1-195">It's a long string that looks something like this:  fdd3b7d3d4f0d2bb2cd3d58dba54bd6bafcd8dee.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-195">It's a long string that looks something like this:  fdd3b7d3d4f0d2bb2cd3d58dba54bd6bafcd8dee.</span></span> <span data-ttu-id="f5fb1-196">A few notes about this:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-196">A few notes about this:</span></span>

* <span data-ttu-id="f5fb1-197">When you create your access token, save it in a text file to make it readily accessible when you need it.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-197">When you create your access token, save it in a text file to make it readily accessible when you need it.</span></span>
* <span data-ttu-id="f5fb1-198">Later, when you need to paste the token, know there are two ways to paste in the command line:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-198">Later, when you need to paste the token, know there are two ways to paste in the command line:</span></span>
  
  * <span data-ttu-id="f5fb1-199">Click the icon in the upper left corner of the command line window>Edit>Paste.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-199">Click the icon in the upper left corner of the command line window>Edit>Paste.</span></span>
  * <span data-ttu-id="f5fb1-200">Right-click the icon in the upper left corner of the window and click Properties>Options>QuickEdit Mode.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-200">Right-click the icon in the upper left corner of the window and click Properties>Options>QuickEdit Mode.</span></span> <span data-ttu-id="f5fb1-201">This configures the command line so you can paste by right-clicking in the command line window.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-201">This configures the command line so you can paste by right-clicking in the command line window.</span></span>

## <a name="install-a-markdown-editor"></a><span data-ttu-id="f5fb1-202">Install a markdown editor</span><span class="sxs-lookup"><span data-stu-id="f5fb1-202">Install a markdown editor</span></span>
<span data-ttu-id="f5fb1-203">We author content using simple "markdown" notation in the files, rather than complex "markup" (HTML, XML, etc.).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-203">We author content using simple "markdown" notation in the files, rather than complex "markup" (HTML, XML, etc.).</span></span> <span data-ttu-id="f5fb1-204">So, you'll need to install a markdown editor.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-204">So, you'll need to install a markdown editor.</span></span>

* <span data-ttu-id="f5fb1-205">**Atom**: Most of us use GitHub's Atom markdown editor: [http://atom.io](http://atom.io).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-205">**Atom**: Most of us use GitHub's Atom markdown editor: [http://atom.io](http://atom.io).</span></span> <span data-ttu-id="f5fb1-206">It does not require a license for business use.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-206">It does not require a license for business use.</span></span> <span data-ttu-id="f5fb1-207">It has spell check.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-207">It has spell check.</span></span>
* <span data-ttu-id="f5fb1-208">**Notepad**: You can use Notepad for a very lightweight option.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-208">**Notepad**: You can use Notepad for a very lightweight option.</span></span>
* <span data-ttu-id="f5fb1-209">**Prose**: This is a lightweight, elegant, on-line, and open source markdown editor that offers a preview.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-209">**Prose**: This is a lightweight, elegant, on-line, and open source markdown editor that offers a preview.</span></span> <span data-ttu-id="f5fb1-210">Visit [http://prose.io](http://prose.io) and authorize Prose in your repository.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-210">Visit [http://prose.io](http://prose.io) and authorize Prose in your repository.</span></span>
* <span data-ttu-id="f5fb1-211">**[Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx)** - Microsoft's entry in this space.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-211">**[Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx)** - Microsoft's entry in this space.</span></span>

## <a name="configure-atom"></a><span data-ttu-id="f5fb1-212">Configure Atom</span><span class="sxs-lookup"><span data-stu-id="f5fb1-212">Configure Atom</span></span>
<span data-ttu-id="f5fb1-213">If you use Atom, you'll need to set a few things up.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-213">If you use Atom, you'll need to set a few things up.</span></span>

* <span data-ttu-id="f5fb1-214">Atom defaults to using 2 spaces for tabs, but Markdown expects 4 spaces.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-214">Atom defaults to using 2 spaces for tabs, but Markdown expects 4 spaces.</span></span> <span data-ttu-id="f5fb1-215">If you leave it at the default of two, your article will look great in local preview, but not when it’s imported into Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-215">If you leave it at the default of two, your article will look great in local preview, but not when it’s imported into Azure.</span></span> <span data-ttu-id="f5fb1-216">So, configure Atom to use 4 spaces - you can find this setting under File>Settings>Editor Settings>Tab Length.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-216">So, configure Atom to use 4 spaces - you can find this setting under File>Settings>Editor Settings>Tab Length.</span></span>
* <span data-ttu-id="f5fb1-217">You will probably also want to turn on Soft Wrap in this section too, which does the same as "word wrap" in Notepad.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-217">You will probably also want to turn on Soft Wrap in this section too, which does the same as "word wrap" in Notepad.</span></span>
* <span data-ttu-id="f5fb1-218">To turn on the markdown preview, click Packages>Markdown Preview>Toggle Preview.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-218">To turn on the markdown preview, click Packages>Markdown Preview>Toggle Preview.</span></span> <span data-ttu-id="f5fb1-219">You can use Ctrl-Shift-M to toggle the preview HTML view.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-219">You can use Ctrl-Shift-M to toggle the preview HTML view.</span></span>

## <a name="fork-the-repository-and-copy-it-to-your-computer"></a><span data-ttu-id="f5fb1-220">Fork the repository and copy it to your computer</span><span class="sxs-lookup"><span data-stu-id="f5fb1-220">Fork the repository and copy it to your computer</span></span>
1. <span data-ttu-id="f5fb1-221">Create a fork of the repository in GitHub - go to the top-right of the page and click the Fork button.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-221">Create a fork of the repository in GitHub - go to the top-right of the page and click the Fork button.</span></span> <span data-ttu-id="f5fb1-222">If prompted, select your account as the location where the fork should be created.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-222">If prompted, select your account as the location where the fork should be created.</span></span> <span data-ttu-id="f5fb1-223">This creates a copy of the repository within your Git Hub account.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-223">This creates a copy of the repository within your Git Hub account.</span></span> <span data-ttu-id="f5fb1-224">Generally speaking, technical writers and program managers need to fork azure-docs-pr, the private repo.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-224">Generally speaking, technical writers and program managers need to fork azure-docs-pr, the private repo.</span></span> <span data-ttu-id="f5fb1-225">Community contributors need to fork azure-docs, the public repo.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-225">Community contributors need to fork azure-docs, the public repo.</span></span> <span data-ttu-id="f5fb1-226">You only need to fork one time; after your first setup, if you want to copy your fork to another computer, you only have to run the commands that follow in this section to copy the repo to your computer.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-226">You only need to fork one time; after your first setup, if you want to copy your fork to another computer, you only have to run the commands that follow in this section to copy the repo to your computer.</span></span>  <span data-ttu-id="f5fb1-227">If you choose to create forks of both repositories, you will need to create a fork for each repository.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-227">If you choose to create forks of both repositories, you will need to create a fork for each repository.</span></span>
2. <span data-ttu-id="f5fb1-228">Copy the Personal Access Token that you got from [https://github.com/settings/tokens](https://github.com/settings/tokens).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-228">Copy the Personal Access Token that you got from [https://github.com/settings/tokens](https://github.com/settings/tokens).</span></span> <span data-ttu-id="f5fb1-229">You can accept the default permissions for the token.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-229">You can accept the default permissions for the token.</span></span>  <span data-ttu-id="f5fb1-230">Save the Personal Access Token in a text file for later reuse.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-230">Save the Personal Access Token in a text file for later reuse.</span></span>
3. <span data-ttu-id="f5fb1-231">Next, copy the repository to your computer with your credentials embedded in the command string.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-231">Next, copy the repository to your computer with your credentials embedded in the command string.</span></span>  <span data-ttu-id="f5fb1-232">To do this, open Git Bash and run it as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-232">To do this, open Git Bash and run it as an administrator.</span></span> <span data-ttu-id="f5fb1-233">At the command prompt, enter the following command.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-233">At the command prompt, enter the following command.</span></span>  <span data-ttu-id="f5fb1-234">This command creates a azure-docs(-pr) directory on your computer.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-234">This command creates a azure-docs(-pr) directory on your computer.</span></span>  <span data-ttu-id="f5fb1-235">If you're using the default location, it will be at c:\users<your Windows user name>\azure-docs(-pr).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-235">If you're using the default location, it will be at c:\users<your Windows user name>\azure-docs(-pr).</span></span>

<span data-ttu-id="f5fb1-236">Public repo:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-236">Public repo:</span></span>

        git clone https://your_GitHub_user_name:your_token@github.com/your_GitHub_user_name/azure-docs.git

<span data-ttu-id="f5fb1-237">Private repo:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-237">Private repo:</span></span>

        git clone https://your_GitHub_user_name:your_token@github.com/your_GitHub_user_name/azure-docs-pr.git

<span data-ttu-id="f5fb1-238">For example, this clone command could look something like this:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-238">For example, this clone command could look something like this:</span></span>

        git clone https://smithj:b428654321d613773d423ef2f173ddf4a312345@github.com/smithj/azure-docs-pr.git  

## <a name="set-remote-repository-connection-and-configure-credentials"></a><span data-ttu-id="f5fb1-239">Set remote repository connection and configure credentials</span><span class="sxs-lookup"><span data-stu-id="f5fb1-239">Set remote repository connection and configure credentials</span></span>
<span data-ttu-id="f5fb1-240">Create a reference to the root repository by entering these commands.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-240">Create a reference to the root repository by entering these commands.</span></span> <span data-ttu-id="f5fb1-241">This sets up connections to the repository in GitHub so that you can get the latest changes onto your local machine and push your changes back to GitHub.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-241">This sets up connections to the repository in GitHub so that you can get the latest changes onto your local machine and push your changes back to GitHub.</span></span> <span data-ttu-id="f5fb1-242">This command also configures your token locally so that you don't have to enter your name and password each time you try to access the upstream repo and your fork on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-242">This command also configures your token locally so that you don't have to enter your name and password each time you try to access the upstream repo and your fork on GitHub.</span></span>

<span data-ttu-id="f5fb1-243">Public repo:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-243">Public repo:</span></span>

        cd azure-docs
        git remote add upstream https://your_GitHub_user_name:your_token@github.com/Microsoft/azure-docs.git
        git fetch upstream

<span data-ttu-id="f5fb1-244">Private repo:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-244">Private repo:</span></span>

        cd azure-docs-pr
        git remote add upstream https://your_GitHub_user_name:your_token@github.com/Microsoft/azure-docs-pr.git
        git fetch upstream

<span data-ttu-id="f5fb1-245">This usually takes a while.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-245">This usually takes a while.</span></span> <span data-ttu-id="f5fb1-246">After you do this, you won't have to fork again or enter your credentials again.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-246">After you do this, you won't have to fork again or enter your credentials again.</span></span> <span data-ttu-id="f5fb1-247">You would only have to copy the forks to a local computer again if you set the tools up on another computer.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-247">You would only have to copy the forks to a local computer again if you set the tools up on another computer.</span></span>

## <a name="configure-your-user-name-and-email-locally"></a><span data-ttu-id="f5fb1-248">Configure your user name and email locally</span><span class="sxs-lookup"><span data-stu-id="f5fb1-248">Configure your user name and email locally</span></span>
<span data-ttu-id="f5fb1-249">To ensure you are listed correctly as a contributor, you need to configure your user name and email locally in Git.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-249">To ensure you are listed correctly as a contributor, you need to configure your user name and email locally in Git.</span></span>

1. <span data-ttu-id="f5fb1-250">Start Git Bash, and switch into azure-docs or azure-docs-pr:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-250">Start Git Bash, and switch into azure-docs or azure-docs-pr:</span></span>
   
   ````
   cd azure-docs
   ````
   
   <span data-ttu-id="f5fb1-251">or</span><span class="sxs-lookup"><span data-stu-id="f5fb1-251">or</span></span>
   
   ````
   cd azure-docs-pr
   ````
2. <span data-ttu-id="f5fb1-252">Configure your user name so it matches your name as you set it up in your GitHub profile:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-252">Configure your user name so it matches your name as you set it up in your GitHub profile:</span></span>
   
    ````
    git config --global user.name "John Doe"
    ````
3. <span data-ttu-id="f5fb1-253">Configure your email so it matches the primary email designated in your GitHub profile; if you're a MSFT employee, it should be your MSFT email address:</span><span class="sxs-lookup"><span data-stu-id="f5fb1-253">Configure your email so it matches the primary email designated in your GitHub profile; if you're a MSFT employee, it should be your MSFT email address:</span></span>
   
    ````
    git config --global user.email "alias@example.com"
    ````
4. <span data-ttu-id="f5fb1-254">Type `git config -l` and review your local settings to ensure the user name and email in the configuration are correct.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-254">Type `git config -l` and review your local settings to ensure the user name and email in the configuration are correct.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5fb1-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5fb1-255">Next steps</span></span>
* <span data-ttu-id="f5fb1-256">Understand the type of content that belongs in the technical content repo, and know what does not belong.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-256">Understand the type of content that belongs in the technical content repo, and know what does not belong.</span></span> <span data-ttu-id="f5fb1-257">See the [content channel guidance](content-channel-guidance.md)!</span><span class="sxs-lookup"><span data-stu-id="f5fb1-257">See the [content channel guidance](content-channel-guidance.md)!</span></span>
* <span data-ttu-id="f5fb1-258">Follow [these steps to create or modify an article and then submit it for publishing](git-commands-for-master.md).</span><span class="sxs-lookup"><span data-stu-id="f5fb1-258">Follow [these steps to create or modify an article and then submit it for publishing](git-commands-for-master.md).</span></span>
* <span data-ttu-id="f5fb1-259">Copy [the markdown template](../markdown templates/markdown-template-for-new-articles.md) as the basis for a new article.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-259">Copy [the markdown template](../markdown templates/markdown-template-for-new-articles.md) as the basis for a new article.</span></span>
* <span data-ttu-id="f5fb1-260">Use [this checklist to verify your pull request will meet the quality criteria](contributor-guide-pr-criteria.md) for merging.</span><span class="sxs-lookup"><span data-stu-id="f5fb1-260">Use [this checklist to verify your pull request will meet the quality criteria](contributor-guide-pr-criteria.md) for merging.</span></span>

### <a name="contributors-guide-navigation"></a><span data-ttu-id="f5fb1-261">Contributors' guide navigation</span><span class="sxs-lookup"><span data-stu-id="f5fb1-261">Contributors' guide navigation</span></span>
* [<span data-ttu-id="f5fb1-262">Overview article</span><span class="sxs-lookup"><span data-stu-id="f5fb1-262">Overview article</span></span>](../README.md)
* [<span data-ttu-id="f5fb1-263">Index of guidance articles</span><span class="sxs-lookup"><span data-stu-id="f5fb1-263">Index of guidance articles</span></span>](contributor-guide-index.md)

<!--Anchors-->
[Use a customer-friendly voice]: #use-a-customer-friendly-voice
[Consider localization and machine translation]: #consider-localization-and-machine-translation
[other style and voice issues to watch for]: #other-style-and-voice-issues-to-watch-for


[Create a GitHub account and set up your profile]: #create-a-github-account-and-set-up-your-profile
[Determine whether you really need to follow the rest of these steps]: #determine-whether-you-really-need-to-follow-the-rest-of-these-steps
[Permissions in GitHub]: #permissions-in-github
[Install Git for Windows]: #install-git-for-windows
[Enable two-factor authentication]: #enable-two-factor-authentication
[Install a markdown editor]: #install-a-markdown-editor
[Fork the repository and copy it to your computer]: #fork-the-repository-and-copy-it-to-your-computer
[Install git-credential-winstore]: #install-git-credential-winstore
[Sign up for Disqus]: #sign-up-for-disqus
[Configure your user name and email locally]: #configure-your-user-name-and-email-locally
[Next steps]: #next-steps
