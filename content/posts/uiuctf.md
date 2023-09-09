# UIUCTF23 Challenge Writeups! 

A long overdue set of writeups (solutions) for UIUCTF23. Recently I had the opportunity to help run UIUCTF 2023, a student-run capture the flag (CTF) event with some awesome folk in SIGPwny. The part I worked on mainly centered around open source intelligence (OSINT) techniques. In this post, we go over some solutions to the OSINT suite as some tips and tricks to approaching these challenges in CTFs. 

### Designing the Challenges 

One of the biggest things I wanted to do while designing these challenges were to be able to tell a story along all the challenges. This set of challenges revolved around the theme of historical figures/places and took the player around different locations in New York and Chicago. Another thing to consider is making sure that these challenges are written in a manner that the first few are approachable and encourage them to approach more challenges. Additionally, it's important to make sure that the challenges are not meant to be written in a guessy manner: they have a clear-cut answer and there are not many potential answers. 

The challenges revolved around from different aspects from Google searches and EXIF data extraction to Zip code encoding and online sleuthing. 

### Finding Artifacts 1
> David is on a trip to collect and document some of the world’s greatest artifacts. He is looking for a coveted bronze statue of the “Excellent One” in New York City. What museum is this located at? The flag format is the location name in lowercase, separated by underscores. For example: uiuctf{statue_of_liberty}

The problem description gives us a general approach to be able to find out where we can get such information. Usually, the first way we want to approach such questions is to just give a brief Google search to see if any information pops up. In our case, we see that by pulling certain keywords out to get a query of: `Bronze Statue “Excellent One” in New York City`: 

![Picture of Chal 1](/uiuctf/excellent.png)

With that, we get the flag of `uiuctf{rubin_museum_of_art}`
### Finding Artifacts 2
> New York City is known for its sprawling subway system. However, none of that would have been possible without modern earth-moving equipment. Find where the first ever shovel was used to start digging the subway. Flag format should be in uiuctf{name_of_museum}

In the same approach as Finding Artifacts 1, we can do a quick Google search to find potential leads to dig deeper into. Pulling out keywords, we see that by searching `First shovel used to dig subway in NYC`, we get that: 

![Shovel 1](/uiuctf/shovel1.png)

However, knowing that, it's not enough since we need to find out where the shovel is actually kept on display. Since we already know it is the *Tiffany Silver Memorial Shovel*, we get that it is located in the `uiuctf{museum_of_the_city_of_new_york}`
### What's For Dinner 
> Jonah Explorer, world renowned, recently landed in the city of Chicago, so you fly there to try and catch him. He was spotted at a joyful Italian restaurant in West Loop. You miss him narrowly but find out that he uses a well known social network and and loves documenting his travels and reviewing his food. Find his online profile.

This one becomes more challenging. Now, you can't take the traditional approach of Googling and getting a direct flag/answer. However, you can see that the main thing to start with is an Italian restauraunt inside of the West Loop. 

![R1](/uiuctf/r1.png)

However, knowing the clue of it being a "joyful" restaurant, we are able to narrow it down to "Gioia Chicago" after searching `Joyful Italian restaurunt in West Loop Chicago.` From there, we know the following facts: 
- He uses a well known social network
- He loves documenting his travels and reviewing his food. 

THe keyword here is "reviewing food." The two main platforms that come to mind for food review are Yelp and Tripadvisor. Let's start by checking those. In Yelp, we see that there are many reviews but how do we narrow them down? By looking through the reviews, we see that Jonah Explorer has left a review with his twitter handle as well!! 

![Yelp2](/uiuctf/yelp2.png)

After obtaining the twitter handle, it becomes smooth sailing from here. We are easily able to extrapolate the tweets from the handle, thus granting us the flag from the first tweet `uiuctf{i_like_spaghetti}`

### Jonah's Journal 

> After dinner, Jonah took notes into an online notebook and pushed his changes there. His usernames have been relatively consistent but what country is he going to next? Flag should be in format uiuctf{country_name}

This was a new take on a challenge. With barely any clues on where to start, the only two main pieces of information are that he "pushed his changes" and that the usernames have been "relatively consistent." If you solved "What's For Dinner" before this challenge, it is fairly straightforward to finish this section. 

The main hint here is that the source if first online, second the term "pushed his changes" suggests that the platform is on GitHub. Since we assume that the player has laready solved "What's for Dinner," they are able to see that his GitHub handle is the same as his twitter `jonahexplorer` with one main repo named `adventurecodes`. Opening it we see that a potential location is China. However, trying out `uiuctf{china}`, we don't get a correct result. 

![Jonah1](/uiuctf/jona1.png)

Looking at it closer, we have another branch. Opening up the branch and commit history, we see a different commit as well with the final flag of `uiuctf{italy}`

![Jonah2](/uiuctf/jona2.png)

### First Class Mail
> Jonah posted a picture online with random things on a table. Can you find out what zip code he is located in? Flag format should be uiuctf{zipcode}, ex: uiuctf{12345}.

![chal](/uiuctf/chal.jpg)

The first obvious trial is the address on the mail in the picture. However, this is merely a honeypot solution intended to distract the user from the true solution. When you look in the middle of the picture, you see a barcode reminiscent of what you see on letters. You can use PostNet encodings to decode it as well. 

![zipcode](/uiuctf/zip.png)

Thus getting us the flag `uiuctf{60661}`

### Finding Jonah
> Jonah offered a reward to whoever can find out what hotel he is staying in. Based on the past information (chals), can you find out what the hotel he stayed at was? Flag should be uiuctf{hotel_name_inn}

![chicago](/uiuctf/chicago.jpeg)

The last challenge gives us a picture and we need to find out where the hotel Jonah is staying at is located. At this point, hopefully one has completed all the challenges previously and this can narrow it down.

In the top right corner of the picture, you can see that there is a Boeing logo there. By using that, we are able to narrow down the region of where the hotel is at based on the proximity it is located. Addtiaionally, if one has completed the previous challenges, they know that the region to look at is West Loop. 

![hotels](/uiuctf/hotel.png)

Using an online map service, we can see that there are different hotels around but only one has a close proximity that makes sense in proximity to the Chicago office. That is the Hilton, thus giving us the flag `uiuctf{hilton}` or `uiuctf{hampton_inn}`

### Ending Notes 

Next up, FallCTF in September 23.

[Back to writing](../../blog)