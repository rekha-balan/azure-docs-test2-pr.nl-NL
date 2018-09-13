# <a name="linking-guidance-for-azure-technical-content"></a><span data-ttu-id="65bfd-101">Linking guidance for Azure technical content</span><span class="sxs-lookup"><span data-stu-id="65bfd-101">Linking guidance for Azure technical content</span></span>
### <a name="links-from-one-article-to-another"></a><span data-ttu-id="65bfd-102">Links from one article to another</span><span class="sxs-lookup"><span data-stu-id="65bfd-102">Links from one article to another</span></span>
<span data-ttu-id="65bfd-103">To create an inline link from one technical article to another technical article, use the following link syntax:</span><span class="sxs-lookup"><span data-stu-id="65bfd-103">To create an inline link from one technical article to another technical article, use the following link syntax:</span></span>  

* <span data-ttu-id="65bfd-104">An article in a service directory links to another article in the same service directory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-104">An article in a service directory links to another article in the same service directory:</span></span>
  
  `[link text](article-name.md)`
* <span data-ttu-id="65bfd-105">An article links from a service subdirectory to an article in the root directory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-105">An article links from a service subdirectory to an article in the root directory:</span></span>
  
  `[link text](../article-name.md)`
* <span data-ttu-id="65bfd-106">An article in the root directory links to an article in a service subdirectory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-106">An article in the root directory links to an article in a service subdirectory:</span></span>
  
  `[link text](./service-directory/article-name.md)`
* <span data-ttu-id="65bfd-107">An article in a service subdirectory links to an article in another service subdirectory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-107">An article in a service subdirectory links to an article in another service subdirectory:</span></span>
  
  `[link text](../service-directory/article-name.md)`

* <span data-ttu-id="65bfd-108">An article links to a .NET API topic:</span><span class="sxs-lookup"><span data-stu-id="65bfd-108">An article links to a .NET API topic:</span></span>

  `[link text](/dotnet/api/type-or-member-name)`

## <a name="links-to-anchors"></a><span data-ttu-id="65bfd-109">Links to anchors</span><span class="sxs-lookup"><span data-stu-id="65bfd-109">Links to anchors</span></span>
<span data-ttu-id="65bfd-110">You do not have to create anchors - they are automatically generated at publishing time for all H2 headings.</span><span class="sxs-lookup"><span data-stu-id="65bfd-110">You do not have to create anchors - they are automatically generated at publishing time for all H2 headings.</span></span> <span data-ttu-id="65bfd-111">The only thing you have to do is create links to the H2 sections.</span><span class="sxs-lookup"><span data-stu-id="65bfd-111">The only thing you have to do is create links to the H2 sections.</span></span>

* <span data-ttu-id="65bfd-112">To link to a heading within the same article:</span><span class="sxs-lookup"><span data-stu-id="65bfd-112">To link to a heading within the same article:</span></span>
  
  `[link](#the-text-of-the-H2-section-separated-by-hyphens)`  
  `[Create cache](#create-cache)`
* <span data-ttu-id="65bfd-113">To link to an anchor in another article in the same subdirectory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-113">To link to an anchor in another article in the same subdirectory:</span></span>
  
  `[link text](article-name.md#anchor-name)`
  `[Configure your profile](media-services-create-account.md#configure-your-profile)`
* <span data-ttu-id="65bfd-114">To link to an anchor in another service subdirectory:</span><span class="sxs-lookup"><span data-stu-id="65bfd-114">To link to an anchor in another service subdirectory:</span></span>
  
  `[link text](../service-directory/article-name.md#anchor-name)`
  `[Configure your profile](../service-directory/media-services-create-account.md#configure-your-profile)`

<span data-ttu-id="65bfd-115">One way to automate the process of creating links in your articles to auto-generated anchor links is [MarkdownAnchorLinkGenerator - a tool to generate anchor links for ACOM in the proper format](https://github.com/Azure/Azure-CSI-Content-Tools/tree/master/Tools/ACOMMarkdownAnchorLinkGenerator).</span><span class="sxs-lookup"><span data-stu-id="65bfd-115">One way to automate the process of creating links in your articles to auto-generated anchor links is [MarkdownAnchorLinkGenerator - a tool to generate anchor links for ACOM in the proper format](https://github.com/Azure/Azure-CSI-Content-Tools/tree/master/Tools/ACOMMarkdownAnchorLinkGenerator).</span></span>

## <a name="links-from-includes"></a><span data-ttu-id="65bfd-116">Links from includes</span><span class="sxs-lookup"><span data-stu-id="65bfd-116">Links from includes</span></span>
<span data-ttu-id="65bfd-117">Since include files are located in another directory, you will need to use longer relative paths as shown below.</span><span class="sxs-lookup"><span data-stu-id="65bfd-117">Since include files are located in another directory, you will need to use longer relative paths as shown below.</span></span> <span data-ttu-id="65bfd-118">To link to an article from an include file, use this format:</span><span class="sxs-lookup"><span data-stu-id="65bfd-118">To link to an article from an include file, use this format:</span></span>

    [link text](../articles/service-folder/article-name.md)

<span data-ttu-id="65bfd-119">Learn more about how to use an include file in the [Custom markdown extensions guidelines](custom-markdown-extensions.md#includes).</span><span class="sxs-lookup"><span data-stu-id="65bfd-119">Learn more about how to use an include file in the [Custom markdown extensions guidelines](custom-markdown-extensions.md#includes).</span></span>

## <a name="links-in-selectors"></a><span data-ttu-id="65bfd-120">Links in selectors</span><span class="sxs-lookup"><span data-stu-id="65bfd-120">Links in selectors</span></span>
<span data-ttu-id="65bfd-121">If you have selectors that are embedded in an include, you would use this sort of linking:</span><span class="sxs-lookup"><span data-stu-id="65bfd-121">If you have selectors that are embedded in an include, you would use this sort of linking:</span></span>

    > [!div class="op_multi_selector" title1="text" title2="text"]
    - [(Text1 | Example1 )](../articles/service-folder/article-name1.md)
    - [(Text1 | Example2 )](../articles/service-folder/article-name2.md)
    - [(Text2 | Example3 )](../articles/service-folder/article-name3.md)
    - [(Text2 | Example4 )](../articles/service-folder/article-name4.md)


## <a name="reference-style-links"></a><span data-ttu-id="65bfd-122">Reference-style links</span><span class="sxs-lookup"><span data-stu-id="65bfd-122">Reference-style links</span></span>
<span data-ttu-id="65bfd-123">You can use reference style links to make your source content easier to read.</span><span class="sxs-lookup"><span data-stu-id="65bfd-123">You can use reference style links to make your source content easier to read.</span></span> <span data-ttu-id="65bfd-124">The reference style links replace the inline link syntax with simplified syntax that allows you to move the long URLs to the end of the article.</span><span class="sxs-lookup"><span data-stu-id="65bfd-124">The reference style links replace the inline link syntax with simplified syntax that allows you to move the long URLs to the end of the article.</span></span> <span data-ttu-id="65bfd-125">Here's Daring Fireball's example:</span><span class="sxs-lookup"><span data-stu-id="65bfd-125">Here's Daring Fireball's example:</span></span>

<span data-ttu-id="65bfd-126">Inline text:</span><span class="sxs-lookup"><span data-stu-id="65bfd-126">Inline text:</span></span>

    I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

<span data-ttu-id="65bfd-127">Link references at the end of the article:</span><span class="sxs-lookup"><span data-stu-id="65bfd-127">Link references at the end of the article:</span></span>

    <!--Reference links in article-->
[1]: http://google.com/
[2]: http://search.yahoo.com/  
[3]: http://search.msn.com/

<span data-ttu-id="65bfd-128">Make sure you include the space after the colon, before the link.</span><span class="sxs-lookup"><span data-stu-id="65bfd-128">Make sure you include the space after the colon, before the link.</span></span> <span data-ttu-id="65bfd-129">When you link to other technical articles, if you forget to include the space, the link will be broken in the published article.</span><span class="sxs-lookup"><span data-stu-id="65bfd-129">When you link to other technical articles, if you forget to include the space, the link will be broken in the published article.</span></span>

## <a name="linking-to-other-microsoft-sites"></a><span data-ttu-id="65bfd-130">Linking to other Microsoft sites</span><span class="sxs-lookup"><span data-stu-id="65bfd-130">Linking to other Microsoft sites</span></span>
<span data-ttu-id="65bfd-131">To link to other Microsoft sites (MSDN, azure.microsoft.com, TechNet), use an absolute URL, but omit the locale.</span><span class="sxs-lookup"><span data-stu-id="65bfd-131">To link to other Microsoft sites (MSDN, azure.microsoft.com, TechNet), use an absolute URL, but omit the locale.</span></span> <span data-ttu-id="65bfd-132">The goal here is that links work in GitHub and on the rendered site:</span><span class="sxs-lookup"><span data-stu-id="65bfd-132">The goal here is that links work in GitHub and on the rendered site:</span></span>

    [link text](http://azure.microsoft.com/pricing/details/virtual-machines/)


### <a name="use-friendly-link-text-for-all-links"></a><span data-ttu-id="65bfd-133">Use friendly link text for all links</span><span class="sxs-lookup"><span data-stu-id="65bfd-133">Use friendly link text for all links</span></span>
<span data-ttu-id="65bfd-134">The words you include in a link should be friendly - in other words, they should be normal English words or the title of the page you are linking to.</span><span class="sxs-lookup"><span data-stu-id="65bfd-134">The words you include in a link should be friendly - in other words, they should be normal English words or the title of the page you are linking to.</span></span> <span data-ttu-id="65bfd-135">Do not use "click here".</span><span class="sxs-lookup"><span data-stu-id="65bfd-135">Do not use "click here".</span></span> <span data-ttu-id="65bfd-136">It's bad for SEO and doesn't adequately describe the target.</span><span class="sxs-lookup"><span data-stu-id="65bfd-136">It's bad for SEO and doesn't adequately describe the target.</span></span>

<span data-ttu-id="65bfd-137">**Correct:**</span><span class="sxs-lookup"><span data-stu-id="65bfd-137">**Correct:**</span></span>

* `For more information, see the [contributor guide index](contributor-guide-index.md).`
* `For more details, see the [SET TRANSACTION ISOLATION LEVEL](https://msdn.microsoft.com/library/ms173763.aspx) reference.`

<span data-ttu-id="65bfd-138">**Incorrect:**</span><span class="sxs-lookup"><span data-stu-id="65bfd-138">**Incorrect:**</span></span>

* `For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).`
* `For more information, click [here](https://github.com/Azure/azure-content/blob/master/contributor-guide/contributor-guide-index.md).`

## <a name="fwlinks"></a><span data-ttu-id="65bfd-139">FWLinks</span><span class="sxs-lookup"><span data-stu-id="65bfd-139">FWLinks</span></span>
<span data-ttu-id="65bfd-140">Avoid FWLinks (our redirection system).</span><span class="sxs-lookup"><span data-stu-id="65bfd-140">Avoid FWLinks (our redirection system).</span></span> <span data-ttu-id="65bfd-141">They should be used only as a last resort when you need to create a link for a page whose URL you don't yet know.</span><span class="sxs-lookup"><span data-stu-id="65bfd-141">They should be used only as a last resort when you need to create a link for a page whose URL you don't yet know.</span></span> <span data-ttu-id="65bfd-142">They are almost never actually needed.</span><span class="sxs-lookup"><span data-stu-id="65bfd-142">They are almost never actually needed.</span></span> <span data-ttu-id="65bfd-143">For technical articles, you define the file name, so you can know what it will be ahead of time.</span><span class="sxs-lookup"><span data-stu-id="65bfd-143">For technical articles, you define the file name, so you can know what it will be ahead of time.</span></span>

<span data-ttu-id="65bfd-144">If you must use an FWLink on a web page, include the P parameter to make it a permanent redirect:</span><span class="sxs-lookup"><span data-stu-id="65bfd-144">If you must use an FWLink on a web page, include the P parameter to make it a permanent redirect:</span></span>

    http://go.microsoft.com/fwlink/p/?LinkId=389595

<span data-ttu-id="65bfd-145">When you paste the target URL into the FWLink tool, remember to remove the locale if your target link is ACOM, or the MSDN or TechNet library.</span><span class="sxs-lookup"><span data-stu-id="65bfd-145">When you paste the target URL into the FWLink tool, remember to remove the locale if your target link is ACOM, or the MSDN or TechNet library.</span></span>

### <a name="contributors-guide-links"></a><span data-ttu-id="65bfd-146">Contributors' Guide Links</span><span class="sxs-lookup"><span data-stu-id="65bfd-146">Contributors' Guide Links</span></span>
* [<span data-ttu-id="65bfd-147">Overview article</span><span class="sxs-lookup"><span data-stu-id="65bfd-147">Overview article</span></span>](../README.md)
* [<span data-ttu-id="65bfd-148">Index of guidance articles</span><span class="sxs-lookup"><span data-stu-id="65bfd-148">Index of guidance articles</span></span>](contributor-guide-index.md)

<!--image references-->
[1]: ./media/create-tables-markdown/table-markdown.png
[2]: ./media/create-tables-markdown/break-tables.png
