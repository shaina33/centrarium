---
layout: post
title:  "Keep your code DRY"
date:   2016-04-11
author: Shaina Karasin
categories: Adventures
tags:	
cover:  "/assets/covers/israel_patio.jpg"
---
It’s been a busy few weeks! My Rails app, a posting & commenting application inspired by Reddit, is coming along nicely. Each day I’m learning how to add new features, such as user roles, favoriting posts, up/down voting, and user-generated category labels. While learning how to implement each of these features is key, it’s also important to keep an eye on the big picture to learn the over-arching concepts that apply across development tasks. One of these concepts is keeping your code DRY, meaning Don’t Repeat Yourself!

I love the DRY concept. It stops you from rewriting the same code as you develop, and it’s a great way to stay organized and efficient as you make changes to your code over time. I like to compare it to using cell references in Excel. In Excel, you could manually look up and re-type a number each time you want to use it.  But maybe you type it incorrectly in one place, and what happens when you need to change that number? You now have to try to find each place the number was used, and properly update it.

A much better option is to write the number only once, and then refer back to it each time it’s needed. In this case, you only have to change it in one place, and you know that the rest of your spreadsheet will update itself accurately. Beautiful! DRY coding is also much easier to read because it involves smaller chunks of code that are clearly labeled regarding their purpose.

To help illustrate the idea of DRY coding, I’ll use one my favorite recent examples: partial views.  In a Rails app, a view is a file containing html and embedded Ruby that instructs how to display a web page in the browser. In my app, I have a User show view to display a user’s profile. It includes information about the user, and then displays their posts, comments, and favorited posts. To write this view file, I could write all of this code from scratch. However, I’ve already needed to display posts and comments elsewhere in my app, so I’ve already written the pieces of code that I need to display a post and a comment. To keep my code elegantly DRY, I can put each of these view code chunks into view partial files, and then just call in the pieces that I need to use in my web pages. 
Here’s a visual example so you can see how to build up partials into larger views, and combine them in different ways.

{% include image.html url="/assets/content/dry_chart.png" %}

DRY coding saves you time during development, and helps you avoid lots of debugging later on. It also helps others to understand your code. Win-win-win. So remember, keep your code DRY!

cover photo: Shaina Karasin, 2014. Tzvat, Israel.