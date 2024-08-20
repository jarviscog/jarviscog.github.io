---
title: 'RFID Hacking Bus Passes'
date: 2024-08-18T15:20:46-04:00
draft: false
tags: ["Projects", "Hardware"]
---

Let me tell you a bit of a story.  

One brisk afternoon I tapped my student card onto the bus to get home from campus. The ride home was a short ten miniute bus ride, with a nice 5 miniute walk home. 

After getting home, I made some food, finished up some homework that was due the following day, and sat down with my roommate to play some Smash Bros. Of course, the new Minecraft Steve DLC was the talk of the town, so we decided to get it and try it out.
After reaching into my pocket, I realized my wallet was gone! I always keep it on me, even around the house, so I was worried right away.
After ripping my room apart, calling the bus company, and asking my roommates if they had seen it, I still couldn't find it.  <br>

Looks like DLC Steve would have to wait. Sighing for the work ahead, I quickly canceled all of my cards, ordered a new driver's license, and went to the website to replace my student card (which doubled as my bus pass).
That's when I found this hidden treasure near the bottom of the page:

{{< highlight text "hl_lines=2" >}}
Lost cards:
    Note: A $40 fee applies for ALL replacement student cards
{{< / highlight >}}
What! You're telling me that my myriad of tuition fees (listed below for comedic effect) doesn't include a replacement card, or at the very least a cheap one!?

{{< detail-tag "Ancillary Fees" >}}

| Description	               | Item Amount (CAD) |
|:-----------------------------|:------------|
| Student Health Plan | 210.01 |
| Student Dental Plan | 202.65 |
| My Virtual Doctor | 44.07 |
| Transit Pass | 288.25 |
| Student Buildings | 69.75 |
| Student Recreation Centre Fund | 46.74 |
| Academic Support incl. Ombuds | 6.78 |
| Health and Wellness | 6.99 |
| Safe Transit Program | 8.83 |
| Government Advocacy | 5.96 |
| Student Life | 8.04 |
| Peer Programs | 2.63 |
| Clubs Administration | 6.52 |
| Student Initiative Grants | 3.15 |
| Student Newspaper | 9.25 |
| Student Radio | 5.57 |
| Student Refugee Program | 0.45 |
| Marching Band Fee | 1.06 |
| Community Legal Services | 3.13 |
| Faculty and Affiliate Councils | 2.32 |
| Financial Aid Office | 20.61 |
| Indigenous Services | 6.48 |
| Student Foot Patrol | 2.54 |
| Recreation | 53.99 |
| Sport | 44.80 |
| Signature Spaces (TRAC) | 10.44 |
| Spirited Activities & Events | 2.86 |
| Student Support & Case Mgmt | 5.01 |
| Wellness & Equity Education | 6.65 |
| Health & Wellness | 56.80 |
| Careers & Experience | 19.27 |
| Academic Support & Engagement | 22.97 |
| International Student Services | 7.56 |
| Off-Campus Housing & Mediation | 4.80 |
| Science Donation | 75.00 |
{{< /detail-tag >}} <br>

All said and done, it took *two weeks* to get the card replaced. I had to send in a new student photo, and they **did not** send me a follow up email, so I had to return to the office three times to check if it was ready.

During my time without a card, I had quite a few chilly bike rides to school to think...

## Getting a Closer Look

What was even in these cards?
From what I understood, it was ~15 grams of plastic, an RFID chip, and maybe the cost of a label maker spread over 10k students. I had no idea why this was such a slow and costly process. 
This got me really curious about how these things actually work, and if I could just make a backup copy of my card to use to get on the bus. The only time I need the actual student card is during an exam. So I could just leave it at home, and use a copy to get to school instead.

The [MFRC522](https://randomnerdtutorials.com/security-access-using-mfrc522-rfid-reader-with-arduino/) looked like a good choice to start this project, but what if we just try using a phone? They already have RFID built-in, and aside from the bus driver knowing something was up, it would mean I could use it instead of any card.  


**NOTE**: This post is currently being written. Come back in a week to read the rest!









