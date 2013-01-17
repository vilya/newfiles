newfiles
========

This is a script which regenerates QtCreator project files after changes occur
outside the IDE, such as checking out from version control.

For generic projects, QtCreator has a file with the extension '.files' which
lists every file in the project. It has a similar file with the extension
'.includes' which lists out all of the directories to search for include files.
When you add or remove a file outside the IDE, you would ordinarily have to
update these files manually to reflect the changes. That gets pretty tedious
when you version control system and a check out may add or remove large numbers
of files.

The docs about generic projects in QtCreator
(http://doc.qt.digia.com/qtcreator-snapshot/creator-project-generic.html)
make the following suggestion:

  "If you frequently need to update the .files file, you can do so efficiently
  by using a script that updates the file for you."

This is such a script. :-)


How it works
------------

When you run this script it will search the file system underneath the project
directory. It will check each file against a whitelist and a blacklist to decide
whether it should be considered part of the project and if so, add it to a list.

It compares this list against the contents of your '.files' file and prints out
a summary of what's been added or removed on the file system.

Finally, if you've specified the '-w' option, it will back up the current
'.files' file and write out a new one using the list built up from the file
system.

It does the same procedure to update the '.includes' file too, except that it
checks directories (rather than files) against a separate whitelist and
blacklist.


Usage
-----

The simplest way to invoke this script is:

  cd MyProject
  newfiles -w
  
If you just want to see what's changed without updating your project files, just
leave off the '-w' argument:

  cd MyProject
  newfiles

These will look for a files with the extensions '.files' and '.includes' in the
current directory.  If there is only one of each, it will use those. Otherwise
you'll need to specify which ones to use:

  newfiles MyProject.files MyProject.includes

There are extra arguments you can provide to customise the whitelists and
blacklists. Use the '-h' option for details:

  newfiles -h


Configuration
-------------

You can add extra command line options to the script on every run by putting
them in a '.newfiles' file. We look in two different locations for this:
- your home directory; and
- the current directory.

If you have a '.newfiles' file in both locations, both get used.

The file is just a text file containing a list of command line arguments, one
per line.


Bugs, feedback and contributions
--------------------------------

The project page for this script is:

  https://github.com/vilya/newfiles

If you have any bug reports or suggestions, please use the issue reporting
system there.

Feel free to fork this code and do what you like with it. Any pull requests will
be gratefully received!
