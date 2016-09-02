---
layout: post
title: Blocipedia
feature-img: "img/cat-reading-book2_Fotor.jpg"
thumbnail-path: "img/cat-reading-book2_editv2.jpg"
short-description: Blocipedia is an application that allows users to create public and private Markdown-based wikis.

---

## Summary
Blocipedia is an application that allows users to create public and private Markdown-based wikis.

## Explanation
For this assignment we were instructed to create an application that works similarly to Wikipedia, which is basically an online encyclopedia based on information provided by users.

## Problem
Some problems I encountered here involved creating the different user levels from free to paid to back to free again if requested by the user. It was also a stumbling block figuring out how to add a collaborator to a PRIVATE Wiki. Say what? :)

## Solution
I was really happy to have figured out how to use Stripe (https://stripe.com/) which was the online payment system for paid membership, and also was psyched to have figured out how to add collaborators to a private wiki by incorporating the "has many through" relationship.

## Results

#### Here are a few images from the final product.

{:.center}
First off, here is the main landing page after signing in. Not very exciting but at least I got the flash notice to work telling the user that they are signed in.

![main page]({{ site.baseurl }}/img/BlocipediaIndexPage.png)

***

Secondly, here is a sample Wiki index page including a button to create a new public or private Wiki.

![Wiki page]({{ site.baseurl }}/img/BlocipediaWikiIndexPage.png)

***

Third, here is an example of the flash warning when the user tries to do something they are not authorized to do. I gotta say those flash notices are sooo simple but I still think they are cool. This was my first taste of having a dynamic webpage so what can I say? I'm psyched.

![Not Authorized]({{ site.baseurl }}/img/BlocipediaNotAuthorized.png)

***

Last but not least, here is an example of the Stripe payment application. Cooleo!

![Stripe]({{ site.baseurl }}/img/BlocipediaStripe.png)

***


## Conclusion
This project started off by reiterating lessons I already learned, such as how to create a page where users can post and delete posts, create private vs. public posts, set up user profiles to log in and out of, and create flash warnings to notify the user when things go well or not. However, in addition, this application taught me how to expand on that base knowledge in how to add collaborators and how to include an online payment system, knowledge that I believe will be useful in the real world.
