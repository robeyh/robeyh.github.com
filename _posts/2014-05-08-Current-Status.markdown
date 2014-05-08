---
layout: post
title: Current Status

---

Display
-------

The display has been working for some time now. The method is relatively
straightforward, text is mapped into an image texture usings the colors of the
pixels to represent the characters. This allows for rather large files to be
displayed and scrolled smoothly at 60 fps with no apparent lag. I loaded in a
100mb text file and everything worked fine. So, all in all, I'm happy with the
way it's able to load in fonts (from Google Web Fonts at the moment, but any
browser loadable font should work), and then display

Vim Macros - Syntax Highlighting
--------------------------------

This... this has been the struggle for the last long while. One of the decisions I made when starting this project was to make sure that my macro system was compatible with Vim macros. I've cycled through iteration after iteration of bad designs to attempt to make this work. Digging into the vim source code for how the macros work has been elucidating. It's fairly obvious that it all grew organically based upon needs. There isn't really an overarching structure. This is visible in the changing structure of the various commands. I haven't been able to write a consistent grammar to parse these pieces.

If anyone has some insight into ways to approach this I would love to hear it. At the moment it's looking to me like the best way to approach it would be to mimic the way Vim evolved. Because of the difference in levels between the code bases this will end up being fairly horribly inefficient, so I welcome alternative thoughts.

Editing
-------

Rudimentary editing works. As does fairly primitive copy-paste. It's not efficient at all. Currently when a change is made I need to update the texture entirely on the CPU side and then resend it to the GPU. For each and every key stroke. I've been working on overhauling this, but I'll make a video in the coming weeks to demonstrate.

Really, this needs to be done by sending only the changes and then modifying the
texture on the GPU itself. I've spent some time prototyping how this might work,
but have yet to integrate the ideas into the project code. The entire chain
should be stored in the browser, with the only communication being the changes
to be made. So undo and redo will all be sent to the GPU anew.

The biggest limitation is the interconnection with the desktop environment. The
browser limits the things that you can do from javascript to prevent various
sorts of trickery. Everyone usually appreciates this because it means that
malicious sites can't pack things into your clipboard. This requires some hacks
in order to work cross browser. Eventually, just writing a plug-in for each
browser may be the best solution to make cut and paste work in the best possible
way. I might just limit myself to Chrome here, making other browsers wait until
the appropriate plug-in can be written. Browsers are also moving towards having
better permissions for this sort of thing. Eventually I might just be able to
ask for it, and once the user confirms have the clipboard access I need. Does
anybody have strong preferences on this? I guess the choice is better cut and
paste in chrome vs. proper cross-browser compatibility.


Swag
----

It has been far too long for this, and I apologize. Many of the original
supporters have likely forgotten or written it off entirely. I hope that
everyone is still using their original kickstarter accounts so that I can get
things to you. I'd like to get the shirts screen printed locally by hand. The
result will be something that looks aged, since the process rarely results in
a perfect print. The same process will be used on the bags.

I'll shoot for getting the surveys out in the two weeks (hopefully next if
reality allows) for people to pick what they want and to provide addresses.

The delays on this were all because I wanted to overcome some hurdles before I
got to it. I wanted to be able to have it coincide with a nearly complete
project. Unfortunately, I put this work into plowing ahead with the idea that 
once I figure out how to implement a strong subset of the vim macro system that
everything else would fall into place. I still believe it's a true statement,
but the implementation is much more daunting that I had imagined... and
reimagined... and reimagined.

Anyway, I apologize for my relative silence. I'm used to being rather thick
skinned, but somewhere along the line the doubt and criticism sunk in. My
usual response... to double down and up the quality enough to shut up naysayers...
wasn't appropriate in this case, and I ended up obsessing over qualities that
didn't further the project at all, to satisfy people that weren't really interested
in things to begin with.
