---
title: 'Autoanki'
date: 2024-08-17T17:55:09-04:00
draft: false
tags: ["Projects"]
hideToc: true
---

## Backstory

For the better part of my Computer Science career I've had a project in the works that I am finally happy to say is \"1.0\".

I was just finishing up my last year of high school when COVID hit. During that time, the school board in my area had the bright idea to fix the grades for each student. As a student, this was pretty awesome, as this meant that I had to do absolutely nothing for the rest of the year, and I would come out with crazy high marks. My friend group and I burned through every video game under the sun, I read a lot, and semi-kept up with the courses I enjoyed.  
At a certian point however, it started to get boring. As a lot of other people chose to do during this time, I decided to try and pick up a foreign language. 
A lot of inspiration to do this came from different youtubers. People like [Xiaoma](https://www.youtube.com/@xiaomanyc), [Steve Kaufmann](https://www.youtube.com/@Thelinguist), and [Langfocus](https://www.youtube.com/@Langfocus) were on repeat around the house. 
I started with Russian, but soon fell in love with Chinese.  

There was a neighbourhood near my house that had a 2nd hand store, and every once in a while I would go in and look at the Chinese books there. 
This started to become an obsession, with me picking up some cryptic book that I couldn't understand just for the fun of it, translating character-by-character trying to get a glimpse into another world. 
Each time I found a word I didn't know, I would add it to an app called Anki on my phone. 
Anki is used to create and store flashcards, and memorize them using the [Spaced Repetition System](https://en.wikipedia.org/wiki/Spaced_repetition). 
{{< figure src="/images/anki-example.jpg" width="600" >}}
**An example Anki card**

Anki shows cards to you based on how well you remembered them the previous time you saw the card. This effectively speeds up memorization of cards, as you see the cards you have trouble remembering a lot move often than the ones you have down-pat.  

This was a great improvement! I could now rest assured knowing that any card I add to my deck I will eventually be able to memorize every character in Chinese.

## Motivation
This was great, however the part that was not great was creating the cards. 
The issue was, it was a *very* manual process, every card needed a character, definition, pronunciation (pinyin), and ideally, the sound as an audio file, and an image. 
There were pre-made decks on the Anki store, but they either:  
- Had too many cards, so now the challenge was filtering out the cards that I was actually going to use
- Did not have all the parts that I wanted, or contained parts that I didn't want  

As a budding Computer Science student going into university, this would not do. I wanted to find a way to quickly create decks.


## Iteration One
Iteration one of the project was decidedly awful. I would go find the book online as a `txt` file, and then run my program with it.
Each step of the program took the previous file and manipulated it. 
In order, it cleaned out all of the non-Chinese characters, put each sentence on a new line, and put the text file into an SQL database.
At the time I thought the problem of splitting a sentence into each word would be too difficult (Chinese does not have spaces) so I split the files into 300kb files, and uploaded it to a website that could do that part for me.  
It was slow, buggy, and hard to debug. The most important thing however, was it was a start. I started to make decks for some of the books in my collection, and was able to successfully use it to understand books at a grade 6 level.

## Iteration Two
Now that I had an idea of how all of the parts were going to work together, I decided to start from the ground up. I trashed the idea of using files for each step, and brought the whole thing into memory. I found a Python library to tokenize the input, and found better ways to get definitions for each word. I created a Python library on `pip` for other people to use it, and started writing documentation.

## Iteration Three
The most recent version of the project is the culmination of four years of computer science. Along with refactoring the code a few times, I:
- Added unit tests
- Got definitions from multiple sources
- Added multiple input file types, such as txt, pdf, and csv
- Created a BLL/DAL scheme
- Created a website to easily use the program
- Added web scrapers to get some books online easier
- Added more card features such as Zhuyin, and easy word filtering
- Improved speed over 10x from the previous iteration
- Made it extendible and easy to add other languages  

It is now at a point where I am happy to say it is a core part of my language learning process.

## Next Steps
I still have big plans for the project which are still in the works. For now, the goal is to make the system faster and more reliable before extending some of the features I have planned.

If you haven't already, give Anki a try. If you find it useful, you may also enjoy autoanki. The link can be found here:
[https://autoanki.netlify.app/](https://autoanki.netlify.app/)
