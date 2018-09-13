---
title: Paper entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Paper entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/31/2017
ms.author: alch
ms.openlocfilehash: 9ee45d7d8c1fa898a8900dfd10f9fec6155e587f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563161"
---
# <a name="paper-entity"></a><span data-ttu-id="edf99-103">Paper Entity</span><span class="sxs-lookup"><span data-stu-id="edf99-103">Paper Entity</span></span>

<span data-ttu-id="edf99-104"><sub> \*Below attributes are specific to paper entity. (Ty = '1') </sub></span><span class="sxs-lookup"><span data-stu-id="edf99-104"><sub> \*Below attributes are specific to paper entity. (Ty = '1') </sub></span></span>


<span data-ttu-id="edf99-105">Name</span><span class="sxs-lookup"><span data-stu-id="edf99-105">Name</span></span>    |<span data-ttu-id="edf99-106">Description</span><span class="sxs-lookup"><span data-stu-id="edf99-106">Description</span></span>                                        |<span data-ttu-id="edf99-107">Type</span><span class="sxs-lookup"><span data-stu-id="edf99-107">Type</span></span>       | <span data-ttu-id="edf99-108">Operations</span><span class="sxs-lookup"><span data-stu-id="edf99-108">Operations</span></span>
------- | ------------------------------------------------- | --------- | ----------------------------
<span data-ttu-id="edf99-109">Id</span><span class="sxs-lookup"><span data-stu-id="edf99-109">Id</span></span>      |<span data-ttu-id="edf99-110">Entity ID</span><span class="sxs-lookup"><span data-stu-id="edf99-110">Entity ID</span></span>                                          |<span data-ttu-id="edf99-111">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-111">Int64</span></span>      |<span data-ttu-id="edf99-112">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-112">Equals</span></span>
<span data-ttu-id="edf99-113">Ti</span><span class="sxs-lookup"><span data-stu-id="edf99-113">Ti</span></span>      |<span data-ttu-id="edf99-114">Paper title</span><span class="sxs-lookup"><span data-stu-id="edf99-114">Paper title</span></span>                                        |<span data-ttu-id="edf99-115">String</span><span class="sxs-lookup"><span data-stu-id="edf99-115">String</span></span>     |<span data-ttu-id="edf99-116">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-116">Equals,</span></span><br/><span data-ttu-id="edf99-117">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-117">StartsWith</span></span>
<span data-ttu-id="edf99-118">L</span><span class="sxs-lookup"><span data-stu-id="edf99-118">L</span></span>       |<span data-ttu-id="edf99-119">Paper language code seperated by "@@@"</span><span class="sxs-lookup"><span data-stu-id="edf99-119">Paper language code seperated by "@@@"</span></span>             |<span data-ttu-id="edf99-120">String</span><span class="sxs-lookup"><span data-stu-id="edf99-120">String</span></span>     |<span data-ttu-id="edf99-121">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-121">Equals</span></span>
<span data-ttu-id="edf99-122">Y</span><span class="sxs-lookup"><span data-stu-id="edf99-122">Y</span></span>       |<span data-ttu-id="edf99-123">Paper year</span><span class="sxs-lookup"><span data-stu-id="edf99-123">Paper year</span></span>                                         |<span data-ttu-id="edf99-124">Int32</span><span class="sxs-lookup"><span data-stu-id="edf99-124">Int32</span></span>      |<span data-ttu-id="edf99-125">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-125">Equals,</span></span><br/><span data-ttu-id="edf99-126">IsBetween</span><span class="sxs-lookup"><span data-stu-id="edf99-126">IsBetween</span></span>
<span data-ttu-id="edf99-127">D</span><span class="sxs-lookup"><span data-stu-id="edf99-127">D</span></span>       |<span data-ttu-id="edf99-128">Paper date</span><span class="sxs-lookup"><span data-stu-id="edf99-128">Paper date</span></span>                                         |<span data-ttu-id="edf99-129">Date</span><span class="sxs-lookup"><span data-stu-id="edf99-129">Date</span></span>       |<span data-ttu-id="edf99-130">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-130">Equals,</span></span><br/><span data-ttu-id="edf99-131">IsBetween</span><span class="sxs-lookup"><span data-stu-id="edf99-131">IsBetween</span></span>
<span data-ttu-id="edf99-132">CC</span><span class="sxs-lookup"><span data-stu-id="edf99-132">CC</span></span>      |<span data-ttu-id="edf99-133">Citation count</span><span class="sxs-lookup"><span data-stu-id="edf99-133">Citation count</span></span>                                     |<span data-ttu-id="edf99-134">Int32</span><span class="sxs-lookup"><span data-stu-id="edf99-134">Int32</span></span>      |<span data-ttu-id="edf99-135">none</span><span class="sxs-lookup"><span data-stu-id="edf99-135">none</span></span>  
<span data-ttu-id="edf99-136">ECC</span><span class="sxs-lookup"><span data-stu-id="edf99-136">ECC</span></span>     |<span data-ttu-id="edf99-137">Estimated citation Count</span><span class="sxs-lookup"><span data-stu-id="edf99-137">Estimated citation Count</span></span>                           |<span data-ttu-id="edf99-138">Int32</span><span class="sxs-lookup"><span data-stu-id="edf99-138">Int32</span></span>      |<span data-ttu-id="edf99-139">none</span><span class="sxs-lookup"><span data-stu-id="edf99-139">none</span></span>
<span data-ttu-id="edf99-140">AA.AuN</span><span class="sxs-lookup"><span data-stu-id="edf99-140">AA.AuN</span></span>  |<span data-ttu-id="edf99-141">Author name</span><span class="sxs-lookup"><span data-stu-id="edf99-141">Author name</span></span>                                        |<span data-ttu-id="edf99-142">String</span><span class="sxs-lookup"><span data-stu-id="edf99-142">String</span></span>     |<span data-ttu-id="edf99-143">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-143">Equals,</span></span><br/><span data-ttu-id="edf99-144">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-144">StartsWith</span></span>
<span data-ttu-id="edf99-145">AA.AuId</span><span class="sxs-lookup"><span data-stu-id="edf99-145">AA.AuId</span></span> |<span data-ttu-id="edf99-146">Author ID</span><span class="sxs-lookup"><span data-stu-id="edf99-146">Author ID</span></span>                                          |<span data-ttu-id="edf99-147">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-147">Int64</span></span>      |<span data-ttu-id="edf99-148">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-148">Equals</span></span>
<span data-ttu-id="edf99-149">AA.AfN</span><span class="sxs-lookup"><span data-stu-id="edf99-149">AA.AfN</span></span>  |<span data-ttu-id="edf99-150">Author affiliation name</span><span class="sxs-lookup"><span data-stu-id="edf99-150">Author affiliation name</span></span>                            |<span data-ttu-id="edf99-151">String</span><span class="sxs-lookup"><span data-stu-id="edf99-151">String</span></span>     |<span data-ttu-id="edf99-152">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-152">Equals,</span></span><br/><span data-ttu-id="edf99-153">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-153">StartsWith</span></span>
<span data-ttu-id="edf99-154">AA.AfId</span><span class="sxs-lookup"><span data-stu-id="edf99-154">AA.AfId</span></span> |<span data-ttu-id="edf99-155">Author affiliation ID</span><span class="sxs-lookup"><span data-stu-id="edf99-155">Author affiliation ID</span></span>                              |<span data-ttu-id="edf99-156">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-156">Int64</span></span>      |<span data-ttu-id="edf99-157">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-157">Equals</span></span>
<span data-ttu-id="edf99-158">AA.S</span><span class="sxs-lookup"><span data-stu-id="edf99-158">AA.S</span></span>    |<span data-ttu-id="edf99-159">Author order for the paper</span><span class="sxs-lookup"><span data-stu-id="edf99-159">Author order for the paper</span></span>                         |<span data-ttu-id="edf99-160">Int32</span><span class="sxs-lookup"><span data-stu-id="edf99-160">Int32</span></span>      |<span data-ttu-id="edf99-161">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-161">Equals</span></span>
<span data-ttu-id="edf99-162">F.FN</span><span class="sxs-lookup"><span data-stu-id="edf99-162">F.FN</span></span>    |<span data-ttu-id="edf99-163">Field of study name</span><span class="sxs-lookup"><span data-stu-id="edf99-163">Field of study name</span></span>                                |<span data-ttu-id="edf99-164">String</span><span class="sxs-lookup"><span data-stu-id="edf99-164">String</span></span>     |<span data-ttu-id="edf99-165">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-165">Equals,</span></span><br/><span data-ttu-id="edf99-166">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-166">StartsWith</span></span>
<span data-ttu-id="edf99-167">F.FId</span><span class="sxs-lookup"><span data-stu-id="edf99-167">F.FId</span></span>   |<span data-ttu-id="edf99-168">Field of study ID</span><span class="sxs-lookup"><span data-stu-id="edf99-168">Field of study ID</span></span>                                  |<span data-ttu-id="edf99-169">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-169">Int64</span></span>      |<span data-ttu-id="edf99-170">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-170">Equals</span></span>
<span data-ttu-id="edf99-171">J.JN</span><span class="sxs-lookup"><span data-stu-id="edf99-171">J.JN</span></span>    |<span data-ttu-id="edf99-172">Journal name</span><span class="sxs-lookup"><span data-stu-id="edf99-172">Journal name</span></span>                                       |<span data-ttu-id="edf99-173">String</span><span class="sxs-lookup"><span data-stu-id="edf99-173">String</span></span>     |<span data-ttu-id="edf99-174">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-174">Equals,</span></span><br/><span data-ttu-id="edf99-175">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-175">StartsWith</span></span>
<span data-ttu-id="edf99-176">J.JId</span><span class="sxs-lookup"><span data-stu-id="edf99-176">J.JId</span></span>   |<span data-ttu-id="edf99-177">Journal ID</span><span class="sxs-lookup"><span data-stu-id="edf99-177">Journal ID</span></span>                                         |<span data-ttu-id="edf99-178">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-178">Int64</span></span>      |<span data-ttu-id="edf99-179">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-179">Equals</span></span>
<span data-ttu-id="edf99-180">C.CN</span><span class="sxs-lookup"><span data-stu-id="edf99-180">C.CN</span></span>    |<span data-ttu-id="edf99-181">Conference series name</span><span class="sxs-lookup"><span data-stu-id="edf99-181">Conference series name</span></span>                             |<span data-ttu-id="edf99-182">String</span><span class="sxs-lookup"><span data-stu-id="edf99-182">String</span></span>     |<span data-ttu-id="edf99-183">Equals,</span><span class="sxs-lookup"><span data-stu-id="edf99-183">Equals,</span></span><br/><span data-ttu-id="edf99-184">StartsWith</span><span class="sxs-lookup"><span data-stu-id="edf99-184">StartsWith</span></span>
<span data-ttu-id="edf99-185">C.CId</span><span class="sxs-lookup"><span data-stu-id="edf99-185">C.CId</span></span>   |<span data-ttu-id="edf99-186">Conference series ID</span><span class="sxs-lookup"><span data-stu-id="edf99-186">Conference series ID</span></span>                               |<span data-ttu-id="edf99-187">Int64</span><span class="sxs-lookup"><span data-stu-id="edf99-187">Int64</span></span>      |<span data-ttu-id="edf99-188">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-188">Equals</span></span>
<span data-ttu-id="edf99-189">RId</span><span class="sxs-lookup"><span data-stu-id="edf99-189">RId</span></span>     |<span data-ttu-id="edf99-190">Referenced papers' ID</span><span class="sxs-lookup"><span data-stu-id="edf99-190">Referenced papers' ID</span></span>                              |<span data-ttu-id="edf99-191">Int64[]</span><span class="sxs-lookup"><span data-stu-id="edf99-191">Int64[]</span></span>    |<span data-ttu-id="edf99-192">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-192">Equals</span></span>
<span data-ttu-id="edf99-193">W</span><span class="sxs-lookup"><span data-stu-id="edf99-193">W</span></span>       |<span data-ttu-id="edf99-194">Words from paper title and Abstract</span><span class="sxs-lookup"><span data-stu-id="edf99-194">Words from paper title and Abstract</span></span>                |<span data-ttu-id="edf99-195">String[]</span><span class="sxs-lookup"><span data-stu-id="edf99-195">String[]</span></span>   |<span data-ttu-id="edf99-196">Equals</span><span class="sxs-lookup"><span data-stu-id="edf99-196">Equals</span></span>
<span data-ttu-id="edf99-197">E</span><span class="sxs-lookup"><span data-stu-id="edf99-197">E</span></span>       |<span data-ttu-id="edf99-198">Extended metadata (see table below)</span><span class="sxs-lookup"><span data-stu-id="edf99-198">Extended metadata (see table below)</span></span>                |<span data-ttu-id="edf99-199">String</span><span class="sxs-lookup"><span data-stu-id="edf99-199">String</span></span>     |<span data-ttu-id="edf99-200">none</span><span class="sxs-lookup"><span data-stu-id="edf99-200">none</span></span>  
        


## <a name="extended-metadata-attributes"></a><span data-ttu-id="edf99-201">Extended Metadata Attributes</span><span class="sxs-lookup"><span data-stu-id="edf99-201">Extended Metadata Attributes</span></span> ##

<span data-ttu-id="edf99-202">Name</span><span class="sxs-lookup"><span data-stu-id="edf99-202">Name</span></span>    | <span data-ttu-id="edf99-203">Description</span><span class="sxs-lookup"><span data-stu-id="edf99-203">Description</span></span>               
--------|---------------------------    
<span data-ttu-id="edf99-204">DN</span><span class="sxs-lookup"><span data-stu-id="edf99-204">DN</span></span>      | <span data-ttu-id="edf99-205">Display Name of the paper</span><span class="sxs-lookup"><span data-stu-id="edf99-205">Display Name of the paper</span></span> 
<span data-ttu-id="edf99-206">S</span><span class="sxs-lookup"><span data-stu-id="edf99-206">S</span></span>       | <span data-ttu-id="edf99-207">Sources - list of web sources of the paper, sorted by static rank</span><span class="sxs-lookup"><span data-stu-id="edf99-207">Sources - list of web sources of the paper, sorted by static rank</span></span>
<span data-ttu-id="edf99-208">S.Ty</span><span class="sxs-lookup"><span data-stu-id="edf99-208">S.Ty</span></span>    | <span data-ttu-id="edf99-209">Source Type (1:HTML, 2:Text, 3:PDF, 4:DOC, 5:PPT, 6:XLS, 7:PS)</span><span class="sxs-lookup"><span data-stu-id="edf99-209">Source Type (1:HTML, 2:Text, 3:PDF, 4:DOC, 5:PPT, 6:XLS, 7:PS)</span></span>
<span data-ttu-id="edf99-210">S.U</span><span class="sxs-lookup"><span data-stu-id="edf99-210">S.U</span></span>     | <span data-ttu-id="edf99-211">Source URL</span><span class="sxs-lookup"><span data-stu-id="edf99-211">Source URL</span></span>
<span data-ttu-id="edf99-212">VFN</span><span class="sxs-lookup"><span data-stu-id="edf99-212">VFN</span></span>     | <span data-ttu-id="edf99-213">Venue Full Name - full name of the Journal or Conference</span><span class="sxs-lookup"><span data-stu-id="edf99-213">Venue Full Name - full name of the Journal or Conference</span></span>
<span data-ttu-id="edf99-214">VSN</span><span class="sxs-lookup"><span data-stu-id="edf99-214">VSN</span></span>     | <span data-ttu-id="edf99-215">Venue Short Name - short name of the Journal or Conference</span><span class="sxs-lookup"><span data-stu-id="edf99-215">Venue Short Name - short name of the Journal or Conference</span></span>
<span data-ttu-id="edf99-216">V</span><span class="sxs-lookup"><span data-stu-id="edf99-216">V</span></span>       | <span data-ttu-id="edf99-217">Volume - journal volume</span><span class="sxs-lookup"><span data-stu-id="edf99-217">Volume - journal volume</span></span>
<span data-ttu-id="edf99-218">I</span><span class="sxs-lookup"><span data-stu-id="edf99-218">I</span></span>       | <span data-ttu-id="edf99-219">Issue - journal issue</span><span class="sxs-lookup"><span data-stu-id="edf99-219">Issue - journal issue</span></span>
<span data-ttu-id="edf99-220">FP</span><span class="sxs-lookup"><span data-stu-id="edf99-220">FP</span></span>      | <span data-ttu-id="edf99-221">FirstPage - first page of paper</span><span class="sxs-lookup"><span data-stu-id="edf99-221">FirstPage - first page of paper</span></span>
<span data-ttu-id="edf99-222">LP</span><span class="sxs-lookup"><span data-stu-id="edf99-222">LP</span></span>      | <span data-ttu-id="edf99-223">LastPage - last page of paper</span><span class="sxs-lookup"><span data-stu-id="edf99-223">LastPage - last page of paper</span></span>
<span data-ttu-id="edf99-224">DOI</span><span class="sxs-lookup"><span data-stu-id="edf99-224">DOI</span></span>     | <span data-ttu-id="edf99-225">Digital Object Identifier</span><span class="sxs-lookup"><span data-stu-id="edf99-225">Digital Object Identifier</span></span>
<span data-ttu-id="edf99-226">CC</span><span class="sxs-lookup"><span data-stu-id="edf99-226">CC</span></span>      | <span data-ttu-id="edf99-227">Citation Contexts – List of referenced paper ID’s and the corresponding context in the paper (e.g. [{123:[“brown foxes are known for jumping as referenced in paper 123”, “the lazy dogs are a historical misnomer as shown in paper 123”]})</span><span class="sxs-lookup"><span data-stu-id="edf99-227">Citation Contexts – List of referenced paper ID’s and the corresponding context in the paper (e.g. [{123:[“brown foxes are known for jumping as referenced in paper 123”, “the lazy dogs are a historical misnomer as shown in paper 123”]})</span></span>
<span data-ttu-id="edf99-228">IA</span><span class="sxs-lookup"><span data-stu-id="edf99-228">IA</span></span>      | <span data-ttu-id="edf99-229">Inverted Abstract</span><span class="sxs-lookup"><span data-stu-id="edf99-229">Inverted Abstract</span></span>
<span data-ttu-id="edf99-230">IA.IndexLength</span><span class="sxs-lookup"><span data-stu-id="edf99-230">IA.IndexLength</span></span>| <span data-ttu-id="edf99-231">Number of items in the index (abstract's word count)</span><span class="sxs-lookup"><span data-stu-id="edf99-231">Number of items in the index (abstract's word count)</span></span>
<span data-ttu-id="edf99-232">IA.InvertedIndex</span><span class="sxs-lookup"><span data-stu-id="edf99-232">IA.InvertedIndex</span></span>| <span data-ttu-id="edf99-233">List of abstract words and their corresponding position in the original abstract (e.g. [{“the”:[0, 15, 30]}, {“brown”:[1]}, {“fox”:[2]}])</span><span class="sxs-lookup"><span data-stu-id="edf99-233">List of abstract words and their corresponding position in the original abstract (e.g. [{“the”:[0, 15, 30]}, {“brown”:[1]}, {“fox”:[2]}])</span></span>