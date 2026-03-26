---
layout: post
title: "Cheaper to Be Wrong"
title-up: "Cheaper to Be Wrong"
title-down: "Validating ideas with AI coding agents"
intro: "Building a working prototype used to be expensive. When the cost drops, the questions you can afford to ask change."
date: 2025-08-2
image: /assets/images/img-26.png
---

A client came to me convinced he had found an angle. The Finnish office rental market, he believed, had room for an aggregator — one that surfaced more granular data than anything currently available. He'd done the thinking. The conviction was real.

The standard move would have been to test it carefully — interviews, demand signals, a landing page. All of that answers a version of the question. None of it answers the version that matters: does the thing actually work when someone uses it.

So instead of researching our way toward a decision, we built. I connected Airtable as a lightweight backend, wired it to a frontend, and within days there was a working prototype in front of real users. Not a mockup. Something you could hand to a landlord and watch.

<div class="post-inline-image-container">
  <img src="/assets/images/offices.png" alt="Office website" class="post-image">
</div>


The prototype was built to test two assumptions. First: would office landlords actually be able to supply the granular data the product depended on? Second: would that data improve conversion — would more detail make users more likely to submit an inquiry?

On the data question: the granular information exists, but it lives inside landlord systems. Surfacing it properly would require integration work on their side — not trivial. For the testing phase, we made the pragmatic call to keep it alive through manual entry. 

On conversion: the hypothesis that richer data would drive more inquiries was weak. The hypothesis that it would filter them was strong. Agents handling inquiries reported meaningfully lower workload — fewer back-and-forth exchanges to establish the basics.

The client now has a real finding instead of a validated assumption. The conversion hypothesis didn't hold. What surfaced instead was a reduction in agent workload — useful, but not a business. The prototype didn't find the idea but it eliminated one path and pointed toward where to look next.

That used to take much longer.