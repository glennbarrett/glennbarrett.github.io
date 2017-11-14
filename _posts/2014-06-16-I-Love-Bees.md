---
layout: post
title:  "My "I Love Bees" write-up from Circle City Con CTF, part of Tri-City CTF"
author: "Glenn"
---

“I love bees” was a cryptology challenge. The files provided were an MP3 file and a JPG file. The JPG was a picture with some stickers that were supposed to be from the cubicle of an employee of the company that had created the audio file, but it also provided some critical hints for the second phase of the challenge. The first thing I did was load the audio file into Audacity, which showed me this: 

![Original](/images/ilovebeesoriginal.gif)

<iframe frameborder="no" height="166" scrolling="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/154632568&color=ff5500&auto_play=false&hide_related=false&show_artwork=true&show_comments=true&show_user=true&show_reposts=false" width="100%"></iframe> 

The right channel (bottom) is basically just a snippet of the track “Flight of the Bumblebee”, however, if you pan to the left track, you can hear some familiar beeping about 40 seconds in. It’s morse code! At first, I attempted to slow the track down enough in Audacity that I could write down the morse as it came across, but then I realized I had a visual representation of the data, so I slowed it waaay down (-80%) and ended up with this: 

![Morse](/images/ilovebeesmorse.gif)

<iframe frameborder="no" height="166" scrolling="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/154633612&color=ff5500&auto_play=false&hide_related=false&show_artwork=true&show_comments=true&show_user=true&show_reposts=false" width="100%"></iframe> 

Note that the actual code was a bit wider than this, but I couldn’t fit it all in one screenshot. The point here is obvious though, because the measurements there are essentially written out morse code. In the end, the entire morse is this: 

<center>**..-. -.-. ---.. ----. -... ..-. -.-. ..--- -... ----- ..... ..-. .---- -.-. ..--- . -.... ....- -... ---.. --... ---.. ....- ...-- ----. ..--- --... ---.. ...-- .- -.-. ----.**</center>

That morse translates to what I hoped would be the flag, but ended up just being a second part of the puzzle: 

<center>**FC89BFC2B05F1C2E64B8784392783AC9**</center>

Now I have a 32 character hexadecimal string, which can be any number of things. I tried running it through some simple online password crackers but none of them liked the format, so then I went back to take a look at the image that was provided with the challenge: 

![Stickers](/images/ilovebees_resized.jpg)

Since the challenge was cryptology, the sticky note with "ECB??" stood out to me. ECB in cryptology is Electronic Codebook, which is a mode of operation for block ciphers. From there, I noticed the 2^7 note, so I thought maybe this was using some sort of 128-bit ECB mode encryption. With this information/hunch, I went to an online decrypter [Tools4Noobs Decrypter](http://www.tools4noobs.com/online_tools/decrypt/) and tried some different keys based on the other sticky notes to decrypt the hexadecimal code. The first key I tried was Archer, due to the sticky note with Mother, Pam, and Cyril since this seemed like a reference to the TV show. That was unsuccessful. I couldn’t really deduce anything from the "I <3 Denver!” or “I’m a Rocket Man” notes, so the only thing left was REDRYDER, which I then tried as the key: 

![Solved](/images/solved.gif)

As you can see, using ECB mode with the Rijndael-128 algorithm, and REDRYDER as the key, the ciphertext decrypted to “FLAG=DAISY”. Daisy is also the manufacturer of Red Ryder BB Guns, and bees tend to like daisies, so that was a nice tie-in. I’m not sure if or how the other notes on the stickies were relevant, but they weren’t necessary to complete the challenge. If anybody has any input, or found out how the other sticky notes may relate to the challenge, let me know in the comments. 

Check out on [@bsjtf](https://twitter.com/bsjtf) Twitter for more challenges and info.