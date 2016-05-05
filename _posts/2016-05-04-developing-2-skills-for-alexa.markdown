---
layout: post
title:  "Developing two skills for Amazon's Alexa"
date:   2016-05-04
author: Shaina Karasin
categories: Adventures
tags:	
cover:  "/assets/covers/seattle-mountains.jpg"
---
As I explained in my [last post](/adventures/2016/05/02/why-is-alexa-interesting.html), I recently started developing voice applications, known as Skills, for the Amazon Alexa service. In this post, I want to provide you with an overview for how Alexa development works, and some of my thoughts on the process. Developing simple apps is surprisingly straightforward, so I encourage everyone to give it a try!

First, there’s the Amazon Developer Portal. This is where you create your skill, provide the descriptive information about it, and create the Voice Interface. This interface has two parts: the Intent Schema, and the Spoken Input Data. The Intent Schema is essentially a list of everything a user might try to do with your skill. Examples from my geography skill include providing a trivia answer, skipping a trivia question, asking Alexa to repeat the trivia question, and ending the game early.

The Spoken Input Data gives Alexa information about what the user might say, and how to interpret it. It includes Sample Utterances, and Custom Values. The Sample Utterances is a list of everything the user might say to Alexa, and which Intent the utterance maps to. For example, with the intent of answering a multiple-choice trivia question, the user might say “My answer is One”, “I choose One”, or simply “One”. This would be three Sample Utterances mapped to one Intent. 

In these Sample Utterances, some words are part of the sentence structure, and some are the key words that the user can change. In the example “My answer is One,” “My answer is…” is the structural part, and “One” is the key word that we need to know to understand what the user is telling us. This is where the Custom Values comes in. It’s a list of all possible values for the key words (called slots) in the user’s speech. In this case, the trivia question has four potential answers, and the user is expected to give the number of their answer, so the Custom Values are just 1,2,3,4. Alexa will determine which intent the user desires (to answer the question) and which slot choice they provided (1), and send that information off to your skill service for processing.

As you can see, you have to think carefully about the voice-based user interaction experience. There are many new concerns due to the medium of voice, such as:
-	the way that numbers are commonly said aloud (1950 does not translate to one thousand nine hundred fifty)
-	the user will make an informal request without being able to see the options you provide, so your skill needs to understand & clarify a wide range of inputs
-	the user cannot receive large amounts of information in audio form, so you need to chunk it in a way that’s manageable
-	Alexa may not pronounce everything correctly, or may use strange intonation, so you must test every part of your skill out loud
-	security for sign-in services (would you want to say your password out loud? Would Alexa understand your weird passwords anyway?)

I find this part of developing for Alexa particularly interesting, as it ties into the Cognitive Science and Psycholinguistics topics that I studied in college. For example, the phonological loop can only keep a limited amount of auditory information in your working memory. Imagine a recorded phone menu that lists 10 options, and you’ll know what I mean. Also, a user will better comprehend Alexa’s words if they receive context upfront, and if there are brief pauses for mental ‘digestion’ after key phrases. This can inform how you phrase your skill’s speech so that the user doesn’t frequently need to ask for repetition. For example, for a trivia question I could write, “What river is the capital city of Kinshasa located on?” However, this puts the key reference word, Kinshasa, at the very end of the sentence and the speech continues on quickly to the possible answers, so the user is likely to ask for a repeat. I can provide a better user experience by writing, “The capital city of Kinshasa, is located on this river:”. Just try to imagine that you’re a game show host reading questions to contestants!

The second major part of your Alexa Skill is the meat of your service, the real coding. This must be hosted somewhere, and the easiest place is on Amazon Web Service Lambda as a Lambda function. AWS Lambda has a free tier that is sufficient to cover all small-time developers. Lambda allows your code to be written in Node.js, Java, or Python. The request will come into your code from Alexa, your code will generate a response, and the response is sent back to Alexa for her to speak aloud.

Luckily for us developers, Amazon has provided the Amazon Skills Kit (ASK), which provides instructions for configuration, and several sample skills written in Node.js or Java. I used two of these templates to create my two skills. Beyond configuring the various pieces, I just had to replace the trivia questions and fun facts with my own content, carefully replace variable names to be relevant, and update the Sample Utterances to fit my content.

Next up on my docket is creating a more customized skill. I still plan to use the ASK samples for guidance, but this time I’ll be choosing a functionality, designing the Voice Interface, figuring out how the backend will work, writing the code, and probably integrating a database. It’s a challenge, but I’m excited for it. Guess I should probably go learn some Node.js!

If you’d like to learn more, these are some great links for getting started:

[Alexa Skills Kit](https://github.com/amzn/alexa-skills-kit-js) on GitHub

[Amazon Developer – ASK](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit)

[Amazon Developer – ASK Sample Skills](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/using-the-alexa-skills-kit-samples)

[Step-by-step instructions to set up a trivia skill]( https://developer.amazon.com/appsandservices/community/post/TxDJWS16KUPVKO/New-Alexa-Skills-Kit-Template-Build-a-Trivia-Skill-in-under-an-Hour)

cover photo: Shaina Karasin, 2013. Hiking near Seattle, WA.