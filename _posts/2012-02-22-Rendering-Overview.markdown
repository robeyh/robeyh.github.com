---

layout: post

title: Icon Selection and Rendering Overview

---

Betwixt Icon Selection
======================

Rachael (@pythonliving) has been busy creating various icon options for voting.  At this point we have a couple to share with you.  Please feel free to submit your own ideas/creations, as well as ideas you would like us to bring to fruition.

Icons
-----

All submissions for icon design will need to be submitted by March 12th.  Voting will begin on the 16th and go through the 19th.  Voting will be processed similar to name voting, and so will take a couple of days to prepare.  Once an icon is selected we will begin swag creation.  At that time everyone will be getting an email verifying address for mailing and other various questions as necessary (T-shirt size, and so on).


Betwixt Update
================


Font Bitmap Overview
--------------------

WebGL does not support fonts at the moment.  However, since we're looking to use monospaced fonts this isn't
too much of an issue.  We do need to somehow create a bitmap font though that can be loaded in as a texture.
We can do this by rendering onto a Canvas element using JavaScript.  Sadly there is no standard way for
JavaScript to access font information at the moment, with the exception being the width of rendered text.  I have
found some tricks to get access to font height but it's not perfect.  The problem is that we can set the font
size, but then to create the bitmap font we need to stuff them all into a gridded picture with each letter
remaining in the proper region.  Currently the code uses reasonable guesses based on the font size, but a method
to caculate the height properly will be needed before it can be considered complete.


Text to Texture Overview
------------------------
Once we have the bitmap font we could render everything as a sprite.  This
could work well.  But it might require more work than is actually necessary.
This is because we would need to attach a position and letter to every sprite.
Additionally, even those letters that are not visible still need to be kept
track of.  This means that either I'm using a static set of sprite objects and
am constantly updating the letters on them and their position as the user
scrolls or I am storing far more letters on the card than are on the screen.

Instead, we can have the entire document be a sprite with a specialized pixel
shader.  This offloads nearly all of the rendering work onto the graphics card
once a little preprocessing is done.  It does require a little math.  The shader
does per pixel calculations.  This is often used to calculate shadows or
transparency.  In this case though we can use them to pick both a letter and an
area of the letter.  The pixel x position mod the letter width gives us the x
position in the document and similarly with the pixel y position mod the letter
height.

We can transform the sequence of letters into a sequence of pixels.  Really this
doesn't require anything other than telling WebGL to assume that it's a picture
and load it in, but a little normalization can minimize the processing required
later.  It also allows for the creation of a secondary helper texture which
stores where the line breaks are.  So we create two textures, one with the contents
of the text file being edited and another that maps a line number to a position
in the text texture.

The mappings go something like this:

pixel y position -> file line number -> texture position

pixel x position -> column in file 

column in file + texture position = letter

And once the textures are created all of this can be done on the graphics card.
However, all editing needs to be done on the computer side and then transferred
again to the graphics card.  Currently this is all done in one large chunk, which
works at a reasonable enough speed for editing bit isn't optimal. I will
need to change this to work in 16k segments for larger files instead.
