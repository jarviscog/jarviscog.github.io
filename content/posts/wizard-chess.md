---
title: 'Wizard Chessboard'
date: 2023-04-20T15:55:09-04:00
draft: false
tags: ["Projects", "Hardware"]
hideToc: true
---
This is a bit of a less technical post, but one that I think is important.  

During my 3rd year I took a group project course called "Object-Oriented Design and Analysis" in which some classmates and I were required to create a project using correct object-oriented design. I was getting an itch to do some more hardware-based projects, and luckily my idea for Wizard Chess got approved.

{{< youtube id=IwjZ1J2b8UY start=23 >}} <br>
  
This was not at all original, as many people have created this idea before, but it seemed both really cool and feasible.
We decided to create the software from the ground up (as that was the class) and base our hardware off of someone else's with some modifications.

## Hardware

The hardware was based on [Greg06's Automated Chessboard](https://www.instructables.com/Automated-Chessboard/) that uses a sort of gantry system with belts. Some of the hardware was bought on Aliexpress, however shipping is *very* slow, so most of the parts had to be ordered on Amazon. 
If I were to do this project again, I may decide to try and make a project in which I already had at least some of the parts, because ordering this sort of thing from Amazon can get expensive real fast.  

The gantry used standard size 20x20 aluminium extrusion, timing belts, and some 3D printed parts.

{{< youtube id="x6VtnNcSBzg" loading="lazy" >}}
**The gantry being held together by me + tape. Notice the slow movement and shaky belts.**

The box to house everything was created with foam, and the top of the board was created with stickers cut on a vinyl cutter. This went relatively smoothly once we got the gantry done.

Inside each piece, a magnet was placed to both move with an electromagnet, and detect when a piece was moved. This turned out to be *agonizingly* finicky, helpfully ilustrated by this wonderful table:

|                            | Magnet Size\-\-    | Magnet Size++         |
|----------------------------|:-------------------|:----------------------|
| __Sensor Sensitivity\-\-__ | Piece not detected | Maybe works           |
| __Sensor Sensitivity++__   | Maybe works        | Pieces detect from other squares |

It was a bit of a balancing act, where *both* variables had to be changed at the same time as to not completely break the system.

## Software

We had ambitious goals for how the software was going to work. Players would put all of the pieces on the board and press a button to start the game. 
Then, the board would connect to LiChess to find a match against a person online. 
The board would move pieces for the online player, while the user would move their own pieces, then press the button.  
The user would then reset the board when the game was complete.

The software side was the real intention of the class, and a lot of the code structure, formatting, and design decisions were made for us. This was so that things lined up with what we were learning in class.

Everything was written in C++, with the use of classes being a requirement. 
Every function or class had to have a docstring, which considerably slowed down development time. 
Many of the other requirements, including test cases seemed to be a bit contrived, as the product we were making realistically only had to work once during the demo.
Code was split up into testable classes, including Game, Board, Stepper motors, and Chess Bot.

With the deadline coming up quick, started to run out of time.  

This meant that we had to do like the power grid, and shed load. Many of the original ideas we had for the project had to get dropped, including the biggest goal, online play through LiChess.

## Lessons Learned

Overall, every one of the group-mates learned a lot from this experience. I came out having two big themes to pull from:

##### A "Just do it" Mentality
One important mentality I had going into the project (and still do) is to *just start*. Even though the final product doesn't look like what we set out to make, it was still a success. 
I came out knowing a lot more about not just the technical stuff like stepper motors and shift registers, but also deadlines, team capabilities, and having realistic expectations.

##### Being able to respond to change
Having a vision for a project is important, however being flexible and able to change is a critical skill to have, particulary in software development. 
This wasn't a lesson that the course explicitly stated, but I'm sure they know that things happen, and one of the soft skills that students would (hopefully) come out of the course having is knowing how to adapt.

> You cannot control the winds; that every sailor knows. But when the favoring wind comes it is your own fault if you do not set your sails to meet it. -- Reverend A. B. Kendig

## Final Result

Overall we were very happy with the result, if a little burnt out by the time crunch. After the submission deadline, a retrospective was due, and I don't think anyone gave it any serious thought. But after some time has passed, I'm glad we made it, and looking forward to take these skills into the next project.

{{< youtube id="tppY0oy66Ag" loading="lazy" >}}
**Důras Gambit. What a move!!**

Thanks for reading! You can find the code for the project [here](https://github.com/jarviscog/Wizard-Chess) and check out the other people that worked on the project:  
[@nollum](https://github.com/nollum) [@Shok302](https://github.com/Shok302)
