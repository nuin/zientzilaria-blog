---
date: '2008-12-10 13:12:04'
layout: post
slug: restoring-original-fonts-on-leopard-as-long-as-you-have-timemachine
status: publish
title: Restoring original fonts on Leopard (as long as you have TimeMachine)
wordpress_id: '219'
categories:
- Misc
---

I've been putting my Vista machine to sleep (I know wrong verb tense, but it's being put to sleep slowly), so I'm transferring some files from it to my main machine at the moment, and some of these files were fonts that work in either system. I had about 1000 free fonts and decided to put install them on my iMac. Of course, something broke and Thunderbird and iTunes started to display text in a cuneiform (or cuneiform-ish) font. So, as a good computer guy I have my system backed up my TimeMachine and I restored the 

/Library/Font 

directory just in case a font was installed over some system font. I used a backup copy of the dir a couple of months old, rebooted the system and voilà! the cuneiform font was still there. Then, I decided to dig deeper, and I searched for how to restore the fonts on Leopard. The less aggressive way I found was to reinstall it. Thanks but no thanks, I thought. Then I decided to dig even deeper (it was getting hot) and I decided to search for the culprit fonts. It wasn't easy among thousands of fonts, so I called spotlight to help me, and searched initially for anything called "fonts" and to my surprise there are two Fonts directories

/Library/Fonts
/>/Library/Fonts 

Checking both, I discovered that the new installed fonts were in the latter and it was also taking precedence over the main system dir. Nice, this makes things even easier, as I just need to remove the fonts from //Library/Fonts and problem solved. And it was!

Disclaimer: I may be dumb (most of the cases you are right) and I also might no read manuals and not have a large knowledge of systems, so if you are the I'm-always-right-and-know-everything-guy from the interwebs, good for you and you shouldn't be reading this anyway. It worked for me so you mileage may vary.Technorati Tags: [fonts](http://technorati.com/tag/fonts), [os x](http://technorati.com/tag/os x), [restoring system](http://technorati.com/tag/restoring system)
