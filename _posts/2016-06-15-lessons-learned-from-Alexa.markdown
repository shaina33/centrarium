---
layout: post
title:  "5 Lessons Learned from the Alexa Project"
date:   2016-06-15
author: Shaina Karasin
categories: Adventures
tags:	
cover:  "/assets/covers/seattle-mountains.jpg"
---
My third Alexa skill, International Calling Codes Directory, was published exactly three weeks ago today!

Unlike my first two Alexa skills, I designed the functionality, built the database, and actually wrote the ‘meat’ of the code, so it was a much larger project. Also, I was coding with JavaScript and Node.js, when I’d never used either before! With this accomplishment, I successfully completed the Bloc/Amazon [Alexa Project](https://developer.amazon.com/public/community/post/Tx2B6EPLOQQB2Y2/Bloc-Launches-Alexa-Project-in-Developer-Bootcamps). While moving on to new projects over the last few weeks, I’ve had some time to reflect on what I learned from developing this third skill, and I’d like to share some of these lessons here.

First, some brief context. This skill is intended to be a handy resource for international calling codes. By this, I mean the +44 (for example) that you need to include when placing an international phone call. The user can ask about a location, and the skill will provide the appropriate calling code(s). Or, the user can ask about a code, and the app will provide the associated location(s). Since this is an Alexa skill, all of the user interaction is done through a flexible voice interface. In the school that I used to work at, we placed & received tons of international phone calls everyday, and this skill would’ve been helpful.

**Moving data from Excel to Amazon DynamoDB**

This turned out to be the largest challenge during development. By scouring Wikipedia, I gathered the location and calling code data that I wanted to use, but I needed to get this data into a database that could be accessed by my skill. My mentor recommended that I use DynamoDB, which is a fast, flexible, noSQL database service offered as part of Amazon Web Services. I searched through lots of Amazon documentation & StackOverflow questions, but the full solution was surprisingly elusive. In the end, I followed this process:  
  
   1. Excel spreadsheet  
   2. Export from Excel as a CSV file (using semicolons as the delimiter)  
   3. Use a simple online converter to change CSV to JSON  
   4. Write a script to upload each entry into DynamoDB  
   5. Run the script using an AWS Lambda function (like my Alexa skills)  

The files that I used to upload JSON into DynamoDB are on my GitHub profile [here]( https://github.com/shaina33/Intnl-Calling-Skill/tree/master/dataTransfer). This seems like a problem that developers would commonly encounter, so I hope my solution can help others!

**Hacking code together only goes so far. Eventually, it’s more efficient to stop and learn a bit about what you’re doing.**

This was my second largest hurdle in the project. For my first two Alexa skills, I didn’t need to write or edit much code, so a very shallow understanding of the code in the templates was sufficient. It wouldn’t have been an effective use of time to study JavaScript syntax or Node.js principles for those skills. So when I started coding for the 3rd skill, I took the same approach. However, this time, I really needed to understand what was happening in the templates, and needed to write my own code. After struggling through it for a few days, making little progress, I finally took a step back and did some research on the fundamentals of JavaScript and Node.js. This turned out to be hugely helpful and got me unstuck ☺ Since I was already comfortable programming in Ruby, I really just needed to learn a few key, missing pieces. I found the following two resources most helpful for learning the pieces I needed quickly:

[w3schools JavaScript Tutorial]( http://www.w3schools.com/js/js_functions.asp) – especially the sections on Functions and Objects  
[Art of Node by Max Ogden]( https://github.com/maxogden/art-of-node) – especially the section on Callbacks

**Carefully plan your application and database design so you don’t have to repeat work.**

While designing my skill, I had to think carefully about what tasks I wanted my skill to accomplish, how my code would actually accomplish these tasks, and how I needed to structure my database to support these tasks. I started developing by first writing an outline containing bullet points and pseudocode to help me think through the details of how the skill would function. I didn’t start gathering my database or coding until this planning process was complete. I feel this was a good strategy, and in the future I would do it even more thoroughly. There were a few times when I realized that something wasn’t going to work quite the way I’d envisioned, and then I had to go through all my data to tweak the arrangement. The better you prepare in advance, the more efficiently you can execute your plan!

**When choosing and designing projects, weigh the amount of work a project/feature will take against the benefits to users. Sometimes, work that’s simpler for you has a larger impact.**

The Amazon Developer portal provides basic usage statistics for each live skill. This has been really fun to follow and see how many real people out in the world are using my creations. For example, my geography skill received 476 utterances from 47 users in its first week! The statistics have also showed me that my first two, simpler skills have received much more usage than my third, more complex skill. This honestly doesn’t surprise me. In this case, I knew that it would have a limited audience, and the primary purpose for the project was expanding my development experience. But in a company setting, it would be important during the planning process to think about which projects can provide the most benefit with the least effort. Just because a project is complex and exciting on the developer’s end, doesn’t mean it’s more awesome for the user.

**Avoid using special characters when possible.**

Alexa is reasonably good at pronunciation; however, she’s not always great with the foreign country names that my skill requires. Luckily, I can instruct her on how to pronounce a word by using [Speech Synthesis Markup Language]( https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/speech-synthesis-markup-language-ssml-reference) to specify English phonemes. In SSML, phonemes can be represented using IPA characters, or using X-SAMPA. I was already familiar with IPA from my college linguistics class, so I initially chose that route. However, I ran into trouble with the special IPA characters translating properly between all the different formats and services that I was using. I ended up going back to my database and changing all of the IPA to X-SAMPA, which uses almost no special characters. X-SAMPA is easier to type initially, and avoids compatibility issues.

cover photo: Shaina Karasin, 2013. Hiking near Seattle, WA.