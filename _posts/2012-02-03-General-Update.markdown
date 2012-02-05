---

layout: post

title: Delayed Update

---

It's been a stressful week.  Lots of non Betwixt things have run through like a herd
of rhinos in my china shop of projects.  I owe people a demonstration/fleshed out status
update and am still working to get something together.

Over the last couple of weeks I've put together a Dropbox library using their REST interface
for saving and loading files.  There was an existing JavaScript library but it required that
the application keys be placed in the open.  I have a sideproject that I'm using to test the
file interfaces that I'll be able to show soon.

I've also made progress on parsing vim files.  I now have a regular expression that shouldn't
have been nearly so hard to create that splits the files into individual command and calls a
different function for each command.  This should also be usable for the in buffer command line.
The next step is writing a state object for each buffer that the commands modify and finally
each command has to be coded as there isn't a particularly hard and fast rule as to how they
must be formed.

Another aspect that I have worked on in yet another set of tests is keyboard input.  I should be
able to roll this into the actual OpenGL tests to update the text rendered to the screen in short
time.

As said, I need a little more time to get a fully fleshed update out.  If Sunday cooperates expect
it then but otherwise it will be early next week.
