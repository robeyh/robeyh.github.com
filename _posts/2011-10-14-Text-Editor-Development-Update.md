---
layout: post

title: Text Editor Development Update

showonfront: false

---

First of all, let's start off with a [screenshot of what the rendering test looks like in Chrome](/images/2011/10/14/shadertest3.png).

This is a test in which a 4MB file (UTF-32, so equivalent to 1MB of ASCII) is loaded and
rendered.  It's able to render at 60 frames per second using requestAnimFrame(), though
given that no updates are occuring this doesn't tell you much other than it's not working
horribly inefficiently.

## Font Rendering and Text Layout in WebGL

The bulk of my effort so far has been here.  I've built multiple experiments trying to
find a good simple way to offload as much of the work of rendering the fonts to the GPU.
I've got a good one.  The text is converted to a texture with each pixel representing a
letter.   An additional texture is necessary to encode the location of line breaks.  The
benefit of doing it this way is that a pixel provides 32 bits of storage, so I can do
UTF-32 as well as highlighting information in the same pixel.  This is as UTF-32 only
actually uses 21 bits per character.  

I then load up a font texture (which is just a standard bitmap font)

All of this loading stuff into textures means that the rendering can all be done in the
fragment shader.  The first thought, and what many bitmap font renderers seem to do is
to store all of the information in the vertex arrays.  This means that 6 vertices are
needed for every letter and I'd need to duplicate information a lot.  It would give me
more flexibility as to positioning, but all of that positioning would have to be done in
the JavaScript and uploaded to the graphics card for each change.  By using the fragment
shader I use 6 vertices to outline the page then each pixel determines which letter it is,
where in the letter it is and what color that location of the letter is.

## Font Loading



## Syntax Highlighting

I was originally split between doing more formal parsing of the text, which
would allow for things like auto-completion and context aware editing to be
based on the actual state of the code instead of heuristics.  The thing is,
I was not able to find a good set of formal grammars for very many languages.
Vim has a very large set of defined syntaxes and writing an interpreter for these
is inline with the other project goals.

## Vim Commands

Vim has a very large set of runtime files using it's internal command system.
Of primary interest are the syntax and indent files.  Then there are also plenty
of macros and all of the extras written by others on the vim site itself.  In
order to use these though the editor needs to understand a subset of the commands
used.  For the syntax files this is primarily the :syntax and :highlight commands.
However, the editor is supposed to be extensible using JavaScript, so here's the
happy medium:  line by line conversion from vim commands to JavaScript.

This has the side-effect of meaning that the command mode for the editor will
accept either vim commands (assuming that a conversion exists) as well as 
javascript macros.  This will be done through a simple construct + algorithm:

/////TODO

## More Syntax Highlighting



## Input

In reviewing existing JavaScript editors I've discovered that all of them use a hack
of somekind with regards to key input.  The problem is that the way this information is
provided to JavaScript is inconsistent and incomplete.  The most direct hack is to use
a textarea and monitor it for changes.  For the moment this is the method that I've been
using for my development.


## File Loading and Saving

Local file loading can be done through Chrome by acquiring access to file:/// urls
(this is just a permission).  Local file saving is a little more difficult.  If we're
willing to restrict ourselves to a sandbox we can do everything, but this will require
that files we wish to edit must be moved to a particular location.  I've yet to start
work on particular loading/saving plugins for online services.

## Summary

I'm not entirely happy with the current rate of progress.  I was hoping that the state
of libraries would be a little further along for this.  Unfortunately, while some WebGL
libraries do support some text, they expect this text to be rendered in the JavaScript
and not to change regularly.  Doing it this way would defeat the purpose of the project.

Additionally, with syntax highlighting and text parsing, each of the existing editors has
not produced a library solely for parsing.  I could take pieces, I've looked at the code
for each, but each seems to define it's own syntax for defining... syntax.  Using a more
established standard instead of reinventing all of this syntax files makes sense.

So, sadly, things are taking more of a "not-developed-here" tack than I'd hoped.

* WebGL text-rendering library
* Vim Command Interpreter
* Vim Compatible Syntax Highlighting


