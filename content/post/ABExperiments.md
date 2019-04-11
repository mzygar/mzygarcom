---
title: "AB Experiments strategy"
date: 2019-04-10T22:49:50+01:00
draft: false
slug: "ab-experiments-strategy"
tags: ["ux","abexperiments"]
image: "images/hans-reniers-746177-unsplash.jpg"
comments: true     # set false to hide Disqus comments
share: true        # set false to share buttons
menu: ""           # set "main" to add this content to the main menu
---

Sometime ago I've had a great discussion with [Danny Ruchtie](https://twitter.com/druchtie) about the AB Experimenting on features.

## Iterative design
It uses *grand design* as a direction we’d like the project to go. However, the changes are introduced iteratively. Each change introduced is atomic. You get a clear picture whether it is improving KPIs or not. If not, you tweak it until you get a positive result. Then test next atomic feature on top of it. The feature choice is complying with the *grand design* direction. You rinse and repeat until you reach (more or less) the design goal. The main disadvantage of this approach is that you are missing out the *synergy effect*, which means that the *grand design* experience would perform better as a whole. So the sum of particular changes changes may perform worse than the actual combination of them (*grand design* aka designed experience)

### Pros
* gives you clear feedback if the  feature improves the metrics or not
* takes less time

### Cons
* you can end up with “good performing mutant” 
* you optimize for KPIs not for the UX
* you may miss the synergy effect


## Designed experience with retrospection
In this approach, we run the test that includes all the changes for the *grand design*.  If the outcome of experiment is negative, we stop it and then we take a step back and run all the atomic features as a separate experiments. The purpose of doing so is to determine what part of the designed experiment worked and what didn’t. So in practice we switch to iterative design approach.

While more time consuming the approach makes use of the designer’s experience to provide best user experience while also improving the KPIs.

To save some headaches all the individual sub-features shall be implemented in the manner that would allow to run as a separate experiment. The dev team should be able to turn it on and off easily.

The only danger I see with this approach is when the experiment is positive, we approve it as a whole. However it might be the case that some parts of it have positive impact and some have negative. So we sacrifice some % of the KPIs improvement in order to provide best user experience. These pain points could be identified via test at later stage.

### Pros
* you optimize for both KPIs and UX
* you control the design of the platform

### Cons
* takes more time
* feedback from experiment is not clear
* you may end up with sub-optimal KPIs improvement in case of synergy is negative


## When to use
Iterative approach is definitely easier one to embrace and could improve the KPIs faster. I’d suggest to use this one when we already have walked the way to the high performing baseline with the pleasurable UX.

If you are just starting the journey towards the high performing baseline with the pleasurable UX, it seems more reasonable to use the Designed experience with retrospection. Once you reach the pleasurable and consistent UX, you could switch to iterative design to optimize all the small things.

After all, all these UX designers are here for a reason, aren’t they?

*//Photo by Hans Reniers on Unsplash*