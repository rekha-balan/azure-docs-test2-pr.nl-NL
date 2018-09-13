# <a name="working-with-release-branches"></a><span data-ttu-id="7c00e-101">Working with release branches</span><span class="sxs-lookup"><span data-stu-id="7c00e-101">Working with release branches</span></span>

<span data-ttu-id="7c00e-102">When you are working with a release branch, the best way to create a local working branch from the release branch is to use this command syntax:</span><span class="sxs-lookup"><span data-stu-id="7c00e-102">When you are working with a release branch, the best way to create a local working branch from the release branch is to use this command syntax:</span></span>

    git checkout -b <local working branch name> upstream/<upstream branch name>

<span data-ttu-id="7c00e-103">This creates the local branch directly from the upstream branch, so you can avoid any local merging.</span><span class="sxs-lookup"><span data-stu-id="7c00e-103">This creates the local branch directly from the upstream branch, so you can avoid any local merging.</span></span>

<span data-ttu-id="7c00e-104">Then, to keep your local copy of the release branch up to date with the upstream version, run:</span><span class="sxs-lookup"><span data-stu-id="7c00e-104">Then, to keep your local copy of the release branch up to date with the upstream version, run:</span></span>

    git pull upstream <release-branch-name>
    
<span data-ttu-id="7c00e-105">To create a copy of the release branch in your online fork, run:</span><span class="sxs-lookup"><span data-stu-id="7c00e-105">To create a copy of the release branch in your online fork, run:</span></span>

    git push origin <release-branch-name>

<span data-ttu-id="7c00e-106">The publishing team runs automation that automatically updates release branches with updates from the master branch on a daily basis.</span><span class="sxs-lookup"><span data-stu-id="7c00e-106">The publishing team runs automation that automatically updates release branches with updates from the master branch on a daily basis.</span></span>

<span data-ttu-id="7c00e-107">When you are ready to merge your changes, you create a pull request from the release branch in your fork to the upstream release branch.</span><span class="sxs-lookup"><span data-stu-id="7c00e-107">When you are ready to merge your changes, you create a pull request from the release branch in your fork to the upstream release branch.</span></span> <span data-ttu-id="7c00e-108">The PR should be set up as shown in the screen shot.</span><span class="sxs-lookup"><span data-stu-id="7c00e-108">The PR should be set up as shown in the screen shot.</span></span>

![](./media/release-branches/release-branch-pr.png)

<span data-ttu-id="7c00e-109">**TIP:** If you receive a *fatal: Cannot update paths and switch to branch 'release-branch' at the same time* error when issuing the `checkout` command, execute `git fetch upstream`, then the checkout command.</span><span class="sxs-lookup"><span data-stu-id="7c00e-109">**TIP:** If you receive a *fatal: Cannot update paths and switch to branch 'release-branch' at the same time* error when issuing the `checkout` command, execute `git fetch upstream`, then the checkout command.</span></span> <span data-ttu-id="7c00e-110">The `fetch` grabs all the new remote-tracking branches (such as the release branch you want to work with) and tags without merging those changes into your own branches.</span><span class="sxs-lookup"><span data-stu-id="7c00e-110">The `fetch` grabs all the new remote-tracking branches (such as the release branch you want to work with) and tags without merging those changes into your own branches.</span></span>