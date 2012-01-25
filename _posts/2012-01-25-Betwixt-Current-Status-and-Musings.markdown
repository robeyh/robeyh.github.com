---

layout: post

title: Betwixt Current Status and Musings

---

We're trying to work on a method of following the release early, release often method.  Our restrictions are the release avenues that we're obliged to follow from the funding model.

We've thought up a couple of different paths to follow for this.

 * Release the code now to the beta crowd under a restrictive license that allows
   no modifications.

 * Release the code now to the beta crowd under a restrictive license that requires
   all modifications can be released under both MIT and LGPL.

 * Release demos that consist of compiled Javascript.  These would serve for 
   demonstration and testing purposes but would not allow for development of code.

 * Release weekly screenshots and videos documenting progress.

 * Write more articles explaining approach and design decisions with code snippets.
   This would allow for more abstract community involvement.


I've spent a lot of time musing over an efficient, maintainable approach for a parser for the vim runtime files.  I've got a couple of different attempts, none of which I'm happy with.  I still think that this is a good approach as it gains access to a large base of definitions and utilities.  These include syntax, keymaps, and autoindent.  The problem is that it's not a scripting language that is all that consistent.

I was hoping to have three pieces: display, editing and syntax highlighting, all working for an initial demonstration.  But I've spent too much time working and reworking the vim command interpreter.  So the first demo will just be display and editing.  Whatever is decided I'll get it to you next week.
