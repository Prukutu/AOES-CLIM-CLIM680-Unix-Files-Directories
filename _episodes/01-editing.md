---
title: "Editing Files"
teaching: 10
exercises: 5
questions:
- "How can I edit files?"
objectives:
- "Learn how to edit files in Linux/Unix."
keypoints:
- "Depending on the type of work you do, you may need a more powerful text editor than Nano."
- "Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file."
---
## Editing files
Let's pick up where we left off, in our `data-shell` directory 
and use `ls -F` to see what it contains:

~~~
$ ls -F
~~~
{: .language-bash}

~~~
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg  solar.pdf  thesis/  writing/
~~~
{: .output}

Last time, we created the `thesis` directory, but there is nothing in it yet:

~~~
$ ls -F thesis
~~~
{: .language-bash}

### Create a text file
Let's change our working directory to `thesis` using `cd`,
then run a text editor called Nano to create a file called `draft.txt`:

~~~
$ cd thesis
$ nano draft.txt
~~~
{: .language-bash}

> ## Which Editor?
>
> When we say, '`nano` is a text editor' we really do mean 'text': it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because it is one of the
> least complex text editors. However, because of this trait, it may
> not be powerful enough or flexible enough for the work you need to do.
>
> On Linux/Unix systems (such including the Unix underlying Mac OS),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which require a bit more time to learn),
> or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). 
>
> No matter what editor you use, it will search within and save files
> to your current working directory as its default location.
{: .callout}

Let's type in a few lines of text.
Once we're happy with our text, in `nano` we can press <kbd>Ctrl</kbd>+<kbd>O</kbd>
(press the <kbd>Ctrl</kbd> or <kbd>Control</kbd> key and, while
holding it down, press the <kbd>O</kbd> key) to write our data to disk
(we'll be asked what file we want to save this to:
press <kbd>Return</kbd> to accept the suggested default of `draft.txt`).

<div style="width:80%; margin: auto;"><img alt="Nano in Action" src="../fig/nano-screenshot.png"></div>

Once our file is saved, we can use <kbd>Ctrl</kbd>+<kbd>X</kbd> to quit the editor and
return to the shell.

> ## The Control, `Ctrl`, or `^` Key
>
> The Control key is often labeled the `Ctrl` key on the keyboard. There are various ways
> in which using the Control key may be described. For example, you may
> see an instruction to press the <kbd>Ctrl</kbd> key and, while holding it down,
> press the <kbd>X</kbd> key, described as any of:
>
> * `Control-X`
> * `Control+X`
> * `Ctrl-X`
> * `Ctrl+X`
> * `^X`
> * `C-x`
>
> In `nano`, along the bottom of the screen you'll see `^G Get Help ^O WriteOut`.
> This means that you can use `Control-G` to get help and `Control-O` to save your
> file.
{: .callout}

`nano` doesn't leave any output on the screen after it exits,
but `ls` now shows that we have created a file called `draft.txt`:

~~~
$ ls
~~~
{: .language-bash}

~~~
draft.txt
~~~
{: .output}

> ## Creating Files in Different Ways
>
> We have seen how to create text files using the `nano` (or ay other) editor, and the `touch` command.
> 
> Programs and scripts can also create files. Most data files are created in this way, 
> including *probably* all of the data files you will use in this class. 
> More about that later.
> 
> Finally, let's see one more way to create a file containing content.
>
> ~~~
> $ echo "Testing" > test.txt
> ~~~
> {: .language-bash}
>
> 1.  What did the `echo` command do (try again but just type `echo "Testing"`)?
>
> > ## Solution
> > 1.  The `echo` command literally echoes the text that follows. 
> >     When nothing else is specified, the text is sent to `stdout` 
> >     i.e., "standard output" - the terminal window. 
> >     
> > 2.  The symbol `>` redirects the output, in this case to a new file
> >     we named `test.txt`
> >
> > 3.  You can inspect the contents of the file `test.txt` by using an editor.
> >     Alternatively, you can print the contents of the file to the terminal
> >     window using the `cat` command: `cat test.txt`.
> >     
> > 4.  Note - only use `cat` in this way if the file is small and contains 
> >     only text characters (no special characters, binary data, etc.).
> >     Otherwise, you may be in for some surprises, or at least a long wait!
> >
> {: .solution}
> 
> Let's try something else. Type this at the command line:
> 
> ~~~
> $ printf "Testing again\nHere is another line.\n" >> test.txt
> ~~~
> {: .language-bash}
> 
> 1.  What happened this time?
>
> > ## Solution
> > 1.  The `printf` command is for "formatted print" and works very much 
> >     like the same command in C or Python (among other languages).
> >     
> > 2.  The symbol `>>` appends the output to the end of the file `test.txt`.
> >     If we had used `>`, the file would have been overwritten.
> >
> > 3.  Within the quoted text, the `\n` is called an **escape sequence**.
> >     The backslash `\` indicates the following character should be 
> >     interpreted as having a special meaning: `\n` means a new line. 
> >     To print the backslash itself in a formatted print, use `\\`.
> >
> {: .solution}
>
{: .challenge}

### If your terminal gets "messed up"...
If you accidentally `cat` a binary file, not only may your screen fill with gibberish,
but your session many get "messed up" (e.g., the text won't clear from your screen, 
your cursor disappears, scrolling behaves incorrectly, or the formatting may have changed).
This happens because some of the binary, when dumped to `stdout`, may have special meanings
that change formatting or other terminal behavior.

You can always clear your screen with the command `clear`. 
This command clears your visible window, but also all prior screen information,
i.e., you will not be able to scroll up and see previous content.

If there are more serious problems with your terminal session, uss the `reset` command.
This will almost always restore your session to working order.


> ## What's In A Name?
>
> You may have noticed that all of the files we are working with are named 'something dot
> something', and in this part of the lesson, we always used the extension
> `.txt`.  This is just a convention: we can call a file `mythesis` or
> almost anything else we want. However, people use two-part names
> most of the time to help them (and their programs) tell different kinds
> of files apart. The second part of such a name is called the
> **filename extension**, and indicates
> what type of data the file holds: `.txt` signals a plain text file, `.pdf`
> indicates a PDF document, `.cfg` is a configuration file full of parameters
> for some program or other, `.png` is a PNG image fime, and so on.
>
> This is just a convention, albeit an important one. Files contain
> bytes: it's up to us and our programs to interpret those bytes
> according to the rules for plain text files, PDF documents, configuration
> files, images, and so on.
>
> Naming a PNG image of a whale as `whale.mp3` doesn't somehow
> magically turn it into a recording of whalesong, though it *might*
> cause the operating system to try to open it with a music player
> when someone double-clicks it.
> 
> Another very handy command is `file`. This command will tell you the format and likely 
> purpose of the file:
> 
> ~~~
> $ file test.txt
> ~~~
> {: .language-bash}
> 
> The `file` command can be used with wildcards to list the types of multiple files
> 
{: .callout}
