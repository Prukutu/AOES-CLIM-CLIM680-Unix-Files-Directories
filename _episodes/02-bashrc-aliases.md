---
title: ".bashrc and aliases"
teaching: 0
exercises: 0
questions:
- "How do I modify the .bashrc file?"
objectives:
- "Customize your bash experience."
- "Define aliases to save you time and typing."
keypoints:
- "Unix shells can be launched in a customized way with the user's preferences."
- "Aliases can be defined that substitute short strings for long or complex commands."
---

### .bashrc

The bash shell allows for a great deal of customization including defining shortcuts for frequently used commands. 
Such preferences are defined in a file in your home directory called `.bashrc`, which is a shell script.
It’s used to save and load your terminal preferences and environmental variables.
In order to load your preferences, bash runs the contents of the `.bashrc` file at each launch. 

Some applications will modify your `.bashrc` file when they are installed or initiated. 
For instance, if you use Anaconda to manage the installation of personal Python or R libraries on your COLA account, 
it will add some scripting code to your `.bashrc` file so that it starts up properly when you login.

Let's take a look at the contents of your `.bashrc` file. Go to your home directory...

~~~
$ cd
$ ls -l .bashrc
-rw------- 1 jdoe123 users 520 Aug 21 13:16 .bashrc
~~~
{: .language-bash}

You will see something like the result above. 

A bit about the information shown when you perform a *verbose* file listing (i.e., using the `-l` option):
* The first ten characters tell you about the nature and permissions of object listed. Permissions are defined at three levels.

  * First character tells what the object is.
    * `-` means it is a file
    * `d` is a directory
    * `l` is a link
    * There are other possibilities here, but these 3 are the most likely ones you will encounter.
    
  * The next 9 characters are 3 sets of 3 that each have the sequence `rwx` and describe the permissions.
    * `r` means *readable* (its contents can be viewed)
    * `w` means *writable* (its contents can be edited and changed)
    * `x` means *executable* (it can be run on the computer)
    * `-` means it is _not_ whichever above.
    
  * The 3 sets of 3 are, in order from left to right:
    * The permissions for the user that owns the file (who created it, or this case ownership was assigned when the account was created).
    * The permissions for any member of the "group" that owns the file (the user is a member of this group).
    * The permissions for anyone who has an account on this computer.
    
  * In this example, `-rw-------` means this is a _file_ that only the reader can read and write. No one else would be able to view or change the contents of this file.

  A user can change the permissions of any file or directory they own.
  
* `1` tells the number of disk blocks occupied, largely irrelevant but can be a useful cue on directories as an indicator of how much data is stored there.

* `jdoe123` is the username of the owner. This is the person who can change file permissions.

* `users` is the group name. A user may belong to multiple groups (e.g., different groups can be set up for different projects with different members), but a directory or file can only be owned by one group, just as it can only be owned by one user.

* `520` is the size of the file in bytes.

* `Aug 21 13:16` is the time the file was altered and saved. After about 6 months without any changes, the timestamp disappears and is replaced by the year.

* `.bashrc` is the file name.

Note that files with names starting with a period are usually system files and are, by default, "hidden". They will not show up with a generic `ls` command unless the `-a` option is used or the file is explicitly named as we did above.

### Adding aliases to .bashrc

Edit `.bashrc` with your preferred editor.

Let's add some aliases. An alias is a command name that is defined to execute another command, set of commands, or execute a script. You can redefine an existing command name to have a different behavior, e.g., to make certain command options act as the defaults when they ordinarily are not. For example, add the following lines at end of the file, which will use the `alias` command to define aliases: 

~~~
alias ls="ls -qx --color=always"
alias ll="ls -al --color=always"
alias lt="ls -alt --color=always | head -10"
~~~
{: .language-bash}

The `alias` command defines a command as the name on the left side of `=` everything that is in the quotation marks on the right, which enclose the command(s) as you would have typed it on the command line. Be sure there are no spaces on either side of `=`. This is a quirk of the `bash` language protocol. 

* The first `alias` command redefines the default settings for the command `ls` so that it won't try to print *unprintable* characters in filenames (`-q`), it switches the way alphabetization is done, so it lists alphabetically across the columns on each line instead of down the columns (`x`) and uses colors to highlight the different kinds of files, directories and permissions (much like what `ls -F` accomplished with symbols).

* The second line defines a new command `ll` that give a "long listing" of the directory contents (`-l`) including the hidden files (`-a`), also using colors.

* The third defines `lt` to give a long listing of the last 10 files or directories to have been changed. This actually uses two commands and *pipes* the result of the `ls` command into the `head` command using the pipe `|`. Pipes are a powerful way to chain commands together into sophisticated operations.

Save the file. The changes will not take effect in your current shell until you re-execute the commands in the `.bashrc` file. You do this with the `source` command:

~~~
$ source .bashrc
~~~
{: .language-bash}

Now try the commands and see how they look!

~~~
$ ls
~~~
{: .language-bash}

To see a list of the aliases you have defined, use the `alias` command with no arguments:

~~~
$ alias
alias ls='ls -qx --color=always'
alias ll='ls -al --color=always'
alias lt='ls -alt --color=always | head -10'
~~~
{: .language-bash}

You can also define an alias by directly typing its definition on the command line. But once you log out (or if your connection is dropped), the alias definition would disappear.

You can make many customizations in addition to defining aliases. You can define the list directories that are in your default PATH when conducting searches for executables, change the way your command line prompt appears, or preload software libraries, to name a few. 

