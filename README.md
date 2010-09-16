Git-Helpers
============

Git-Helpers is a collection of little scripts (currently just one, but hey!) generally useful to Git users.

Using the scripts
-----------------

The scripts should run just about everywhere, as they are pure-Ruby.  Just drop them in a directory that is part of your PATH environment variable, make sure they have execution permissions, and you're ready to go!

Still, you need Ruby.

### Ruby

I went to great pains not to require anything more than that: no Rubygems, etc..  You also probably need to have your `git` binary in your default execution path.

If you're on a Linux, UNIX or OS X box, you most likely have a recent-enough version of Ruby installed already.  Just check by typing the following in a command line:

	$ ruby -v
	ruby 1.8.7 (2009-06-12 patchlevel 174) [universal-darwin10.0]

Any Ruby from 1.8.6 on is fine.  If you don't have it installed (what kind of system is that?!), [head over here](http://www.ruby-lang.org/en/downloads/) and install it; it's pretty fast and painless.

The scripts
-----------

There is currently just one script, but I'll be posting more as I stratch more itches :-)

### `git-svn-migrate-ignores`

This is for people who have to deal with remote Subversion repositories.  Git only handles the `svn:executable` property; everything else, most notably `svn:ignore`, is, well… ignored (Git actually says they are "unhandled").

Whether you're just migrating a hitherto SVN repo to the joys of Git, or are simply alleviating the pain of SVN by using Git locally over an active Subversion repository, you probably need to keep your `.gitignore` files in sync with your `svn:ignore` properties.  This only goes one way, however, as Git won't let us set Subversion properties; and I didn't want to sync stuff back up, if only to avoid having to rely on a command-line `svn`.

You can run this script anytime, from anywhere within your Git repository.  It will always *sync the whole "trunk"*, though, grabbing whatever unhandled `svn:ignore` were reported by Git for your trunk, and creating, or updating, your `.gitignore` files accordingly.

It won't add your `.gitignore` files to the index automatically, in case you want to keep those local, or prefer to add them manually for whatever reason.

A typical run may look like this:

	$ git-svn-migrate-ignores
	Processing .git/svn/trunk/unhandled.log…
	  [=] config: Unchanged.
	  [=] data: Unchanged.
	  [=] db: Unchanged.
	  [=] log: Unchanged.
	  [M] public: Adding leguide_fr.txt.
	  [C] public/images: Adding svn:ignore.
	  [M] public/images: Adding brands / carriers / faq_custom / wish_images / wish_lists.
	  [=] public/images/categories: Unchanged.
	  [=] public/images/categories/fullsize: Unchanged.
	  [=] public/images/categories/small_thumb: Unchanged.
	  [M] tmp: Adding attachment_fu / inline / restart.txt.
	  [=] tmp/cache: Unchanged.
	  [=] tmp/pids: Unchanged.
	  [=] tmp/sessions: Unchanged.
	  [=] tmp/sockets: Unchanged.

* The `[C]` marker means your `.gitignore` file was created on-the-fly.
* The `[M]` marker means it got updated, because it didn't contain all the entries from the matching `svn:ignore` property.
* The `[=]` marker means it was left untouched, as it contained all the necessary entries (and possibly more, which is fine).

So there you have it!  Don't ignore what you should ignore.  Well, you know what I mean :-)

Licence
-------

This is licenced under the MIT licence, listed below and at the top of the script.  The executive summary goes: do whatever you want with it, except strip the copyright or licence info from it.

	Copyright (c) 2010 Christophe Porteneuve <tdd@git-attitude.fr>
	
	Permission is hereby granted, free of charge, to any person obtaining a copy
	of this software and associated documentation files (the "Software"), to deal
	in the Software without restriction, including without limitation the rights
	to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
	copies of the Software, and to permit persons to whom the Software is
	furnished to do so, subject to the following conditions:
	
	The above copyright notice and this permission notice shall be included in
	all copies or substantial portions of the Software.
	
	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
	THE SOFTWARE.

Contributing
------------

People, this is open-source, using plain old Ruby, and it's posted on Github.  Fork away and be merry!

Happy Git'ing,

(s.) Christophe