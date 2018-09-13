# <a name="git-commands-for-creating-a-new-article-or-updating-an-existing-article"></a><span data-ttu-id="dce70-101">Git commands for creating a new article or updating an existing article</span><span class="sxs-lookup"><span data-stu-id="dce70-101">Git commands for creating a new article or updating an existing article</span></span>
## <a name="standard-process-working-from-master"></a><span data-ttu-id="dce70-102">Standard process (working from master)</span><span class="sxs-lookup"><span data-stu-id="dce70-102">Standard process (working from master)</span></span>
<span data-ttu-id="dce70-103">Follow the steps in this article to create a local working branch on your computer so that you can create a new article for the Azure technical documentation section of docs.microsoft.com/azure or update an existing article.</span><span class="sxs-lookup"><span data-stu-id="dce70-103">Follow the steps in this article to create a local working branch on your computer so that you can create a new article for the Azure technical documentation section of docs.microsoft.com/azure or update an existing article.</span></span>

1. <span data-ttu-id="dce70-104">Start Git Bash (or the command-line tool you use for Git).</span><span class="sxs-lookup"><span data-stu-id="dce70-104">Start Git Bash (or the command-line tool you use for Git).</span></span>
   
   <span data-ttu-id="dce70-105">**Note:** If you are working in the public repository, change azure-docs-pr to azure-docs in all the commands.</span><span class="sxs-lookup"><span data-stu-id="dce70-105">**Note:** If you are working in the public repository, change azure-docs-pr to azure-docs in all the commands.</span></span>
2. <span data-ttu-id="dce70-106">Change to azure-docs-pr:</span><span class="sxs-lookup"><span data-stu-id="dce70-106">Change to azure-docs-pr:</span></span>
   
        cd azure-docs-pr
3. <span data-ttu-id="dce70-107">Check out the master branch:</span><span class="sxs-lookup"><span data-stu-id="dce70-107">Check out the master branch:</span></span>
   
        git checkout master
4. <span data-ttu-id="dce70-108">Create a fresh local working branch derived from the master branch:</span><span class="sxs-lookup"><span data-stu-id="dce70-108">Create a fresh local working branch derived from the master branch:</span></span>
   
        git pull upstream master
        git checkout -B <working branch>
5. <span data-ttu-id="dce70-109">Let your fork know you created the local working branch:</span><span class="sxs-lookup"><span data-stu-id="dce70-109">Let your fork know you created the local working branch:</span></span>
   
        git push origin <working branch>
6. <span data-ttu-id="dce70-110">Create your new article or make changes to an existing article.</span><span class="sxs-lookup"><span data-stu-id="dce70-110">Create your new article or make changes to an existing article.</span></span> <span data-ttu-id="dce70-111">Use Windows Explorer to open and create new markdown files.</span><span class="sxs-lookup"><span data-stu-id="dce70-111">Use Windows Explorer to open and create new markdown files.</span></span> <span data-ttu-id="dce70-112">After you create or modify your article and images, go to the next step.</span><span class="sxs-lookup"><span data-stu-id="dce70-112">After you create or modify your article and images, go to the next step.</span></span>
7. <span data-ttu-id="dce70-113">Add and commit the changes you made:</span><span class="sxs-lookup"><span data-stu-id="dce70-113">Add and commit the changes you made:</span></span>
   
        git add --all
        git commit –m "<comment>"
   
   <span data-ttu-id="dce70-114">Or, to add only the specific files you modified:</span><span class="sxs-lookup"><span data-stu-id="dce70-114">Or, to add only the specific files you modified:</span></span>
   
        git add <file path>
        git commit –m "<comment>"
8. <span data-ttu-id="dce70-115">Update your local working branch with changes from the upstream master branch:</span><span class="sxs-lookup"><span data-stu-id="dce70-115">Update your local working branch with changes from the upstream master branch:</span></span>
   
        git pull upstream master
9. <span data-ttu-id="dce70-116">Push the changes to your fork on GitHub:</span><span class="sxs-lookup"><span data-stu-id="dce70-116">Push the changes to your fork on GitHub:</span></span>
   
        git push origin <working branch>
       
10. <span data-ttu-id="dce70-117">When you are ready to submit your content to the upstream master branch for staging, validation, and/or publishing, in the GitHub UI, create a pull request from your fork to the master branch.</span><span class="sxs-lookup"><span data-stu-id="dce70-117">When you are ready to submit your content to the upstream master branch for staging, validation, and/or publishing, in the GitHub UI, create a pull request from your fork to the master branch.</span></span>
11. <span data-ttu-id="dce70-118">If you are an employee working in the private repository, the changes you submit are automatically staged and a staging link is written to the pull request.</span><span class="sxs-lookup"><span data-stu-id="dce70-118">If you are an employee working in the private repository, the changes you submit are automatically staged and a staging link is written to the pull request.</span></span> <span data-ttu-id="dce70-119">Please review your staged content and sign off in the pull request comments by adding the **#sign-off** comment.</span><span class="sxs-lookup"><span data-stu-id="dce70-119">Please review your staged content and sign off in the pull request comments by adding the **#sign-off** comment.</span></span>  <span data-ttu-id="dce70-120">This indicates the changes are ready to be pushed live.</span><span class="sxs-lookup"><span data-stu-id="dce70-120">This indicates the changes are ready to be pushed live.</span></span>  <span data-ttu-id="dce70-121">If you don't want the pull request to be accepted - if you are just staging the changes - add the **#hold-off** note to the pull request.</span><span class="sxs-lookup"><span data-stu-id="dce70-121">If you don't want the pull request to be accepted - if you are just staging the changes - add the **#hold-off** note to the pull request.</span></span>
12. <span data-ttu-id="dce70-122">If your update is small in scope, the PR may qualify for automatic merge.</span><span class="sxs-lookup"><span data-stu-id="dce70-122">If your update is small in scope, the PR may qualify for automatic merge.</span></span> <span data-ttu-id="dce70-123">If not, the pull request review team reviews your pull request, provides feedback, and merges it if the PR meets [the minimum quality criteria](contributor-guide-pr-criteria).</span><span class="sxs-lookup"><span data-stu-id="dce70-123">If not, the pull request review team reviews your pull request, provides feedback, and merges it if the PR meets [the minimum quality criteria](contributor-guide-pr-criteria).</span></span>

## <a name="publishing"></a><span data-ttu-id="dce70-124">Publishing</span><span class="sxs-lookup"><span data-stu-id="dce70-124">Publishing</span></span>
* <span data-ttu-id="dce70-125">Articles are published at approximately 10:00 AM and 3:00 PM Pacific Time, Monday-Friday.</span><span class="sxs-lookup"><span data-stu-id="dce70-125">Articles are published at approximately 10:00 AM and 3:00 PM Pacific Time, Monday-Friday.</span></span> <span data-ttu-id="dce70-126">It can take up to 30 minutes for articles to appear online after publishing.</span><span class="sxs-lookup"><span data-stu-id="dce70-126">It can take up to 30 minutes for articles to appear online after publishing.</span></span> <span data-ttu-id="dce70-127">Remember your pull request has to be merged by a pull request reviewer before the changes can be included in the next scheduled publishing run.</span><span class="sxs-lookup"><span data-stu-id="dce70-127">Remember your pull request has to be merged by a pull request reviewer before the changes can be included in the next scheduled publishing run.</span></span> <span data-ttu-id="dce70-128">You need to work with your pull request reviewer ahead of time to ensure a pull request is merged for a specific publishing run.</span><span class="sxs-lookup"><span data-stu-id="dce70-128">You need to work with your pull request reviewer ahead of time to ensure a pull request is merged for a specific publishing run.</span></span> <span data-ttu-id="dce70-129">Otherwise, PRs are reviewed in the order they were submitted.</span><span class="sxs-lookup"><span data-stu-id="dce70-129">Otherwise, PRs are reviewed in the order they were submitted.</span></span>
* <span data-ttu-id="dce70-130">If you are an employee working in the private repository, all pull requests are subject to validation rules that need to be addressed before the pull request can be merged.</span><span class="sxs-lookup"><span data-stu-id="dce70-130">If you are an employee working in the private repository, all pull requests are subject to validation rules that need to be addressed before the pull request can be merged.</span></span>