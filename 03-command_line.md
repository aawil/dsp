# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> > `pwd`: show current working directory

> > `mkdir`: create a directory

> > `rmdir` or `rm -r`: delete a directory

> > `touch filename`: create a file

> > `rm`: delete a file

> > `mv`: rename a file

> > `ls -a`: list hidden files

> > `cp dir1/file dir2/`: copy a file from one directory to another

> > `echo "text"`: output text to stdout

> > `clear`: make everything all clean and new again

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> > `ls`: list files in current directory

> > `ls -a`: list all files (including .hidden files)

> > `ls -l`: list files in long format (showing permissions, size, modified date, etc.)

> > `ls -lh`: same as above, but shows file sizes with units

> > `ls -lah`: same as above, but shows .hidden files

> > `ls -t`: orders output by last modified (recent first)

> > `ls -Glp`: list files in long format, with slashes indicating directories, and also pretty colors

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > `ls -lS`: sort files by size

> > `ls -lT`: show excruciatingly detailed last modified info

> > `ls -A`: like -a, but skips the . and .. 'directories'

> > `ls -x`: sorts multi-column output across first instead of down first. Alias to 'ls' to annoy your friends

> > `ls -i`: show each file's social security number

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > xargs takes text as input and does a given command on each 'item' in the text (separated by spaces, newlines, or what have you). For example:

> > `echo "big chungus" | xargs touch` will create two files called `big` and `chungus`. This isn't very useful, but you can pipe stuff like the output of a grep or find into xargs to save a lot of time.
 

