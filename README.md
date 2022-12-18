# Simple_Shell
The shell is a command line interface (CLI) program that takes commands from the keyboard and gives them to the operating system to perform.

The Shell
Material by Milad Fatenejad, Sasha Wood, Radhika Khetani and Karin Lagesen

Modified by Shoaib Sufi for Manchester, 2014 and by Seb James for Sheffield 2015

This tutorial
This is a tutorial to introduce you to the shell and how it might be useful for your research.

You can use a browser to open this tutorial on github: https://github.com/mikeg64/linux_shell/shell

#Introduction As a result Linux is available on many types of machines from super computers to PCs. Currently UBUNTU is the flavour of Linux that has gained great popularity The UNIX operating system was developed in the early 1970s by a group of enthusiasts at Bell Laboratories in the USA. Since then it was modified by a number of different groups and evolved into many similar but not identical flavours. Linus Torvalds, at the time a computer science student at the university of Helsinki, started a freely available academic version of UNIX ‘LINUX’ that was to become the standard for all Linux implementations that followed. Now-a-days Unix and Linux have become almost synonymous with each other. Linux is structured so that the user works within a ‘shell’ that can be configured by the system administrators, working behind the scenes. LINUX is a multi-user, multi-tasking operating system, which has the following features:

Hierarchical File System
Process Management
Command Interpreter (Shell)
What is a shell?
A shell is a program which reads a command that you typed; decides what to do with it; does it; then prints out any text that was generated.

It's a middleman between you and the core (or kernel) of the computer.

A terminal is a program that gives you access to the shell - think of the terminal as the window enclosing the shell, and the shell as that little prompt at the bottom:

`you@somecomputer:~$`
The shell we'll use is called bash. Although there are others, bash is the most commonly used shell. The shell can be viewed as an interpreted computer programming language with a focus on interactive use.

What the shell does: It calls built-in commands and programs
Usually, when you type a command at the shell, all you want the shell to do is to find, and execute a program.

For example, ps is a standalone program which gives you some information about the processes running on the computer:

ps
When you type this, the shell first checks if ps is one of its own, special built-in keywords. It then looks in its list of "places where there might be programs" and runs the first one it finds. (That list is called the PATH; more on that later).

You can see the ps program that you just ran by listing it:

ls /bin/ps
Some commands you'll use are bash builtins. A couple of examples are alias and source. When you type these, you activate code which is part of the shell itself. This is also true of programming constructs such as conditionals (if/else), loops, variable assignments and so on.

For historical reasons, most important Linux commands are only two letters long. This brevity can sometimes make them difficult to remember, and it is not always easy to tell from a sequence of commands exactly what is happening. Also Linux distinguishes upper case letters from lower case, and insists that many commands are written in lower case. Typing a command in upper case will probably generate the response

Command not found
A typical Linux command consists of a general command word, which may be followed by optional parameters that specify more precisely what you want the command to do. Many of these options consist of a single letter, making the command brief but not altogether easy to remember. If a command operates on files then the filenames must come after the options.

command [option …] [filename …]
The Example: Manipulating Experimental Data Files
We will spend most of our time learning about the basics of the shell by manipulating some experimental data from a hearing test.

To get the data:

git clone https://github.com/mikeg64/linux_shell.git
The git command will grab all of the data needed for this workshop from GitHub.

Now we'll change directory into the directory tree which git cloned for us:

cd linux_shell
Moving around the file system
The filesystem is like a tree. On Unix systems, there's only one root of the tree (the analogy ends at the ground). Windows systems may have several trees (C:\ D:\ and so on). The bottom of the tree is called the root and in Unix, it's represented by the symbol '/'

Navigating the filesystem at the shell requires some typing, but there are a number of shortcuts and conveniences to ease the pain.

First we have to know where we are. The program pwd (print working directory) tells you where you are sitting in the directory tree. The command ls will list the files in the current directory. Directories are often called "folders" because of how they are represented in GUIs. Directories are just listings of files. They can contain other files or directories.

When you start up a terminal on most systems, you will start in a special directory called the home directory. If you're using the managed desktop, you'll initially find yourself in a Desktop directory, so change to your home:

cd
Every user has their own home directory where they have full access to create and delete files and directories. At the start of a session the pwd command tells us what the name of our home directory is. The last word in that listing should also be the name of your user. You can also find out your user name by entering the command whoami.

You can always get back to your home directory by typing cd (return).

File Types
When you enter the ls command, it lists the contents of the current directory. There are several items in your home directory.

Let's create an empty file using the touch command. Enter the command:

touch testfile
Then list the contents of the directory again. You should see that a new entry, called testfile, exists. The touch command just creates an empty file.

touch is Super Useful! Why? because it updates the last-modified date of the file. This can be useful in scripts to check if you need to carry out some function or other, perhaps on data being generated by another program.

To get a fuller listing, add the -l switch. This will show the file size, the owner and information about the permissions applied to the file. If the entry is a directory, then the first letter will be a "d". The fifth column shows you the size of the entries in bytes. Notice that testfile has a size of zero.

Try ls -l -h (or equivalently ls -lh). That makes the file size show up in "human readable" format.

Now, let's get rid of testfile. To remove a file, just enter the command:

rm testfile
The rm command can be used to remove files. If you enter ls again, you will see that testfile is gone.

Changing Directories
Now, let's move to a different directory. The command cd (change directory) is used to move around. We used cd earlier to get us into the linux_shell directory. Now let's move into the shell directory. Enter the following command:

cd shell
Now use the ls command to see what is inside this directory. This directory contains all of the material for the shell part of this boot camp. Now move to the directory containing the data for the shell tutorial:

cd data
If you enter the cd command by itself, you will return to the home directory. Try this, and then navigate back to the shell directory.

Arguments
Most programs take additional arguments that control their exact behavior. For example, -F and -l are arguments to ls. The ls program, like many programs, take a lot of arguments. But how do we know what the options are to particular commands?

Most commonly used shell programs have a manual. You can access the manual using the man program. Try entering:

man ls
This will open the manual page for ls. Use the space key to go forward and b to go backwards. When you are done reading, just hit q to exit.

Note: if you are using Git Bash on Windows you will not have access to man. People have hosted the man pages at various sites which is useful for people on any platform e.g www.kernel.org/doc/man-pages/online_pages.html or www.linuxmanpages.com

Programs that are run from the shell can get extremely complicated. To see an example, open up the manual page for the find program, which we will use later this session. No one can possibly learn all of these arguments, of course. So you will probably find yourself referring back to the manual page frequently. Note: sometimes it can be pretty difficult to understand what it says in a man file. However, each time you read a man file you will understand more of it.

Job control
Most programs, like ls and cd finish very quickly and output their results immediately. Some programs last a long time and may output their results into a file, so they'll sit there holding your command line hostage until they finish. To allow long lived programs to be executed without losing access to the command line, most shells have a form of job control built in.

If a job is run in the foreground, then access to the command line is suspended until the job finishes. By default, a command you run at the shell will run in the foreground.

A job can be run in the background, in which case it will give the command line back to you for the execution of additional commands.

To run a job in the background, add an & after the command:

ps &
This is particularly useful for graphical programs which open up their own window, or for running a program a few times in parallel.

ps & ps & 
If you put an interactive program like an editor into the background, it'll effectively disappear. GNU Nano is a text editor which is both common and easy to use. Try it out: open it with

nano
and then exit with Ctrl-x. As we don't have nano on the Managed Desktop, you can use vi for this example. vi is more common than nano, but much more confusing for new users:

vi
You have to exit vi with :q!.

Now run it in the background:

nano &
or

vi &
Not so useful. You see the shell outputs the editor's job number and also its process id. You can list the current running jobs with

jobs
If it's job 1, then you can bring it into the foreground with

%1
You can stop the job with Ctrl-z and then put it into the background with bg or into the foreground with fg.

You can kill a stopped job with

kill %1
Assuming it was job number 1.

Examining the contents of other directories
By default, the ls commands lists the contents of the working directory (i.e. the directory you are in). However, you can also give ls the names of other directories to view. Navigate to the home directory if you are not already there. Then enter the command:

ls linux_shell
This will list the contents of the linux_shell directory without you having to navigate there. Now enter:

ls linux_shell/shell
This prints the contents of shell. The cd command works in a similar way. Try entering:

cd linux_shell/shell
and you will jump directly to shell without having to go through the intermediate directory.

Absolute vs. Relative Paths
The cd command takes an argument which is the directory name. Directories can be specified using either a relative path or an absolute path. The directories on the computer are arranged into a hierarchy. The absolute path tells you where a directory is in that hierarchy, all the way from the root and up.

Navigate to the home directory. Now, enter the pwd command and you should see the full name of your home directory. This tells you that you are in a directory that is named the same as your user, which sits inside one or more other directories. The very top of the hierarchy is a directory called / which is usually referred to as the root directory.

First, figure out again what the absolute path to your home directory was. Now enter the following command (replace the stuff in <> with the results from pwd).

cd <pwd-results>/linux_shell/shell
This jumps to shell. Now go back to the home directory. We saw earlier that the command

cd linux_shell/shell
had the same effect - it took us to the shell directory. But, instead of specifying the absolute path which started with a /, we specified a relative path. In other words, we specified the path relative to our current directory. A absolute path always starts with a /. A relative path does not. You can usually use either an absolute path or a relative path depending on what is most convenient. If we are in the home directory, it is more convenient to just enter the relative path since it involves less typing.

Now, list the contents of the /bin directory. Do you see anything familiar in there?

Saving time with shortcuts, wild cards, and tab completion
Shortcuts
There are some shortcuts which you should know about. Referring to the home directory is very common. The shell recognises the tilde character, ~, as a shortcut for your home directory. Navigate to the shell directory, then enter the command:

ls ~
This prints the contents of your home directory, without you having to type the absolute path. The shortcut .. always refers to the directory above your current directory. Thus:

ls ..
prints the contents of the ~/linux_shell directory. You can chain these together, so:

ls ../../
prints the contents of what should be your home directory. Finally, the special directory . always refers to your current directory. So, ls, ls ., and ls ././././. all do the same thing, they print the contents of the current directory. This may seem like a useless shortcut right now, but we'll see when it is needed in a little while.

To summarize, the commands ls ~, ls ~/., ls ../../, and ls <absolute path to home directory> all do exactly the same thing. These shortcuts are not necessary, they are provided for your convenience.

Our data set: Cochlear Implants
A cochlear implant is a small electronic device that is surgically implanted in the inner ear to give deaf people a sense of hearing. More than a quarter of a million people have them, but there is still no widely-accepted benchmark to measure their effectiveness. In order to establish a baseline for such a benchmark, teenagers with CIs were asked to listen to audio files on their computer and report:

the quietest sound they could hear
the lowest and highest tones they could hear
the narrowest range of frequencies they could discriminate
To participate, test subjects were played an audio sample by a lab tech who then recorded their data - when the subjects first heard the sound, or first heard a difference in the sound. Each set of test results were written out to a text file, one set per file. Each participant has a unique subject ID, and a made-up subject name. Each experiment has a unique experiment ID. The experiment has collected 351 files so far.

The data is a bit of a mess! There are inconsistent file names, there are extraneous "NOTES" files that we'd like to get rid of, and the data is spread across many directories. We are going to use shell commands to get this data into shape. By the end we would like to:

Put all of the data into one directory called "alldata"

Have all of the data files in there, and ensure that every file has a ".txt" extension

Get rid of the extraneous "NOTES" files

Globbing with wild cards [Super useful]
Navigate to the ~/linux_shell/shell/data/THOMAS directory. This directory contains our hearing test data for THOMAS. If we type ls, we will see that there are a bunch of files which are just four digit numbers. By default, ls lists all of the files in a given directory. The * character is a shortcut for "everything". Thus, if you enter ls *, you will again see all of the contents of a given directory. This * can be combined with other characters. Now try this command:

ls *1
This lists every file that ends with a 1. This command:

ls /usr/bin/*.sh
Lists every file in /usr/bin that ends in the characters .sh.

This command:

ls *4*1
lists every file in the current directory which contains the number 4, and ends with the number 1. There are four such files: 0241, 0341, 0431, and 0481.

So how does this actually work? When the shell (and this is a bash-specific explanation; other shells may vary) sees a word that contains the * character, it automatically looks for files that match this wild card; * means "anything". In this case, it identified four such files. Then, it replaced the *4*1 with the list of files, separated by spaces and passes that as the argument list to the program. In other words, the two commands:

ls *4*1
ls 0241 0341 0431 0481
result in an identical call to ls. The ls command cannot tell the difference between these two things.

The expansion of wild cards by the shell is known as globbing. There are some other wild cards beyond the * character which you can search up on the internet.

Short Exercise
Do each of the following using a single ls command without navigating to a different directory.

List all of the files in /bin that contain the letter a
Can you figure out if there are any directories inside of /bin?
More on expansion: quotation marks and spaces in filenames [Super Useful]
Spaces are important when you type commands in the shell:

cd ../.. # To go back to the 'shell' directory
This command lists two files:

ls 4fileone 4filetwo
This command lists one file:

ls "4fileone 4filetwo"
The shell interprets the quotation marks and passes the string "4fileone 4filetwo" to the ls program.

This is how you can refer to a file containing a space. Another way is to "escape the space":

ls 4fileone\ 4filetwo
The backslash there tells the shell to interpret the space as part of the string and not as the separator between one argument and another.

Dealing with spaces is a bit annoying on the command line, which is why most Linux and Unix users tend to avoid spaces in their file names.

Lastly,

ls '4fileone 4filetwo'
Is similar to ls "4fileone 4filetwo", but has an important difference. Try this:

ls "$HOME"
and this:

ls '$HOME'
Short Exercise
Work through the above examples which used ls, replacing ls with cat. This should prove that the quotation marks are important and that the use of spaces in filenames is inadvisable.

Tab Completion [Super useful]
Navigate to the home directory. Typing out directory names can waste a lot of time. When you start typing out the name of a directory, then hit the tab key, the shell will try to fill in the rest of the directory name. For example, enter:

cd 2<tab>
The shell will fill in the rest of the directory name for linux_shell. Press enter to enter the boot camp directory. Next, go into the shell directory and do:

ls 3<tab><tab>
When you hit the first tab, nothing happens. The reason is that there are multiple file in this directory which start with 3. Thus, the shell does not know which one to fill in. When you hit tab again, the shell will list the possible choices.

Tab completion can also fill in the names of programs. For example, enter e<tab><tab>. You will see the name of every program that starts with an e. One of those is echo. If you enter ec<tab> you will see that tab completion works.

Command History
You can easily access previous commands. history (a bash built-in) lists the command history.

[seb@sebpad 08:48:28 shell]$ history
 (Extra output snipped)
 2053  ls
 2054  which history
 2055  history
[seb@sebpad 08:48:45 shell]$ 
You can re-call a command from that history like this:

!2053
This will call ls from the short list above.

Navigating and searching the command history [Super useful]
You can quickly access recent commands from the history and search the history:

Hit the up arrow. Hit it again. You can step backwards through your command history. The down arrow takes you forwards in the command history.

^-C will cancel the command you are writing, and give you a fresh prompt.

^-R will do a reverse-search through your command history. This is very useful. If you find a partial match you can keep pressing ^-R until you find the instance you are interested in.

Which program?
Commands like ls, rm, and cd are just ordinary programs on the computer. A program is just a file that you can execute. The program which tells you the location of a particular program. For example:

which ls
Will return "/bin/ls". Thus, we can see that ls is a program that sits inside of the /bin directory. Now enter:

which find
You will see that find is a program that sits inside of the /bin directory (it might be /usr/bin on some platforms).

You could have an executable program anywhere on the filesystem. When we enter a program name, like ls, and hit enter, how does the shell know where to look for that program?

How does it know to run /bin/ls when we enter ls and not /home/me/usr/bin/ls?

The answer is that when we enter a program name and hit enter, there are a few standard places that the shell automatically looks. If it can't find the program in any of those places, it will print an error saying "command not found". Enter the command:

echo $PATH
This will print out the value of the PATH environment variable. Notice that a list of directories, separated by colon characters, is returned. These are the places the shell looks for programs to run. If your program is not in this list, then an error is printed. The shell ONLY checks in the places listed in the PATH environment variable.

Note: You can modify the PATH environment variable; adding special directories containing the programs you have written; this is super useful on Iceberg, where you can't install programs into /bin or /usr/bin

Navigate to the shell directory and list the contents. You will notice that there is a program (executable file) called hello in the shell directory. Now, try to run the program by entering:

hello
You should get an error saying that hello cannot be found. That is because the directory <your home directory>/linux_shell/shell is not in the PATH (this is actually a security feature). However, it turns out that in Windows git bash, the current working directory IS in the path.

In any case, you can run the hello program by entering:

./hello
Remember that . is a shortcut for the current working directory. This tells the shell to run the hello program which is located right here. So, you can run any program by entering the path to that program. You can run hello equally well by specifying:

<path to home directory>/linux_shell/shell/hello
Or by entering:

../shell/hello
While you're at it; try:

$HOME/linux_shell/shell/hello
and

/home/$USER/linux_shell/shell/hello
Neat huh? HOME and USER are two more examples of environment variables.

When there are no / characters, the shell assumes you want to look in one of the default places for the program.

Calling MatLab from the shell
This section can't be run with the Sheffield Windows Managed Desktop *
In can be convenient to call MatLab from the command line.

For me the location of matlab was /Applications/MATLAB_R2013a.app/bin/matlab. If running matlab produces a command not found type of message then you can either use the absolute path for matlab or you can add it to your PATH which is the list of locations that the shell searches for commands and programs:

MATLAB_LOCATION=/Applications/MATLAB_R2013a.app/bin
export PATH=$MATLAB_LOCATION:$PATH
You can put these lines into your .bashrc file to have them run every time you log in

Now using nano or notepad make a file called hello.m and put the following contents in and save the file:

disp('hello')
exit()
Then from the same directory call the following command:

matlab -nosplash -nodesktop -r hello -logfile out.txt
This calls matlab without a GUI, the filename is hello.m but the argument to -r is just hello and the output is written to stdout and a file called out.txt - you can use nano or cat to check the contents.

Another way of calling MatLab is by using a Here Document. The Here Document redirects the output of a command block into the stdin of a program or command. In our current example, rather than putting the list of commands in a file and then calling matlab you can place them in the following way:

matlab -nosplash -nodesktop <<HEREMARKER
disp('hello')
exit()
HEREMARKER         
One benefit of this approach is that you can keep all of your MatLab and bash commands in one file if this were a script.

For more information about Here Documents please refer to The LDP's Advanced Bash-Scripting Guide

Short Exercise
Using the above example write a Here Document based script for MatLab, modify it's permissions and run it to test that it works.

Calling the shell from matlab
Learning about the shell is useful because it makes it easier to call external programs from matlab scripts. When you use the system() call in matlab, it actually launches a shell, then passes the content of the system() call's argument to the shell, meaning you can do things like:

[status, stdout] = system ('ls ~/somedir/');
This assumes that your matlab is installed on Linux or Mac; the Windows matlab system call won't call a bash shell; instead it calls the standard DOS shell.

You can shortcut to calling a shell command with the ! character in matlab:

! ls
Examining Files
We now know how to switch directories, run programs, and look at the contents of directories, but how do we look at the contents of files?

The easiest way to examine a file is to just print out all of the contents using the program cat. Enter the following command:

cat ex_data.txt
This prints out the contents of the ex_data.txt file. This file contains an example of how our data is formatted. If you enter:

cat ex_data.txt ex_data.txt
It will print out the contents of ex_data.txt twice. cat just takes a list of file names and writes them out one after another (this is where the name comes from, cat is short for concatenate).

Short Exercises
Print out the contents of the ~/linux_shell/shell/dictionary.txt file. What does this file contain?

Without changing directories, (you should still be in shell), use one short command to print the contents of all of the files in the <your home directory>/linux_shell/shell/data/THOMAS directory.

cat is a terrific program, but when the file is really big, it can be annoying to use. Try this:

cat  ~/linux_shell/shell/dictionary.txt
All you can see is about the last 25 lines of that file. How to see the previous lines?

One way is to scroll up in your terminal or [Super useful tip] press Shift-PgUp), but this has limitations (one is that neither works on the Windows Managed Desktop's installation of git bash!).

The file viewing program, less, is a good tool for viewing long files. Enter the following command:

less ~/linux_shell/shell/dictionary.txt
less opens the file, and lets you navigate through it. The commands are identical to the man program. Use "space" to go forward and hit the "b" key to go backwards. The "g" key goes to the beginning of the file and "G" goes to the end. When you are done, hit "q" to quit.

less also gives you a way of searching through files. Just hit the "/" key to begin a search. Enter the word you would like to search for and hit enter. It will jump to the next location where that word is found. Try searching the dictionary.txt file for the word "cat". If you hit "/" then "enter", less will just repeat the previous search. less searches from the current location and works its way forward. If you are at the end of the file and search for the word "cat", less will not find it. You need to go to the beginning of the file and search.

Remember, the man program uses the same commands (in fact, it uses less as its viewer!), so you can search documentation using "/" as well.

Short Exercise
Use the commands we've learned so far to figure out how to search in reverse while using less.

Redirection
Let's turn to the experimental data from the hearing tests. This data is located in the ~/linux_shell/shell/data directory. Each subdirectory corresponds to a particular participant in the study. Navigate to the Bert subdirectory in data. First, press ls to look at the files. There are a bunch of text files which contain experimental data results. Lets print them all:

cat *
Now enter the following command:

cat * > ../all_data
This tells the shell to take the output from the cat * command and dump it into a new file called ../all_data. To verify that this worked, examine the all_data file. If all_data had already existed, we would overwritten it. So the > character tells the shell to take the output from whatever is on the left and dump it into the file on the right. The >> characters do almost the same thing, except that they will append the output to the file if it already exists.

Short Exercise
Use >>, to append the contents of all of the files whose name contains the number 4 in the directory:

<your home directory>/linux_shell/shell/data/gerdal
to the existing all_data file. Thus, when you are done all_data should contain all of the experiment data from Bert and any experimental data file from gerdal that contains the number 4.

Creating, moving, copying, and removing
We've created a file called all_data using the redirection operator >. This file is critical - it's our analysis results - so we want to make copies so that the data is backed up. Lets copy the file using the cp command. The cp command backs up the file. Navigate to the data directory and enter:

cp all_data all_data_backup
Now all_data_backup has been created as a copy of all_data. We can move files around using the command mv. Enter this command:

mv all_data_backup /tmp/
This moves all_data_backup into the directory /tmp. The directory /tmp is a special directory that all users can write to. It is a temporary place for storing files. Data stored in /tmp may be automatically deleted when the computer shuts down.

The mv command is also one way to rename files. Since this file is so important, let's rename it:

mv all_data all_data_IMPORTANT
Type in ls, and you will see that file name has been changed to all_data_IMPORTANT. Let's delete the backup file now:

rm /tmp/all_data_backup
The mkdir command is used to create a directory. Just enter mkdir followed by a space, then the directory name.

Short Exercise
Do the following:

Rename the all_data_IMPORTANT file to all_data.
Create a directory in the data directory called foo
Then, copy the all_data file into foo
Do ls foo to have a look inside the new directory
By default, rm, will NOT delete directories. You can tell rm to delete a directory using the -r option. Enter the following command:

rm -r foo
Count the words
The wc program (word count) counts the number of lines, words, and characters in one or more files. Make sure you are in the data directory, then enter the following command:

wc Bert/* gerdal/*4*
For each of the files indicated, wc has printed a line with three numbers and also the relative file name. The first is the number of lines in that file. The second is the number of words. Third, the total number of characters is indicated. The bottom line contains this information summed over all of the files. Thus, there were 10445 characters in total.

Remember that the Bert/* and gerdal/*4* files were merged into the all_data file. So, we should see that all_data contains the same number of characters:

wc all_data
Every character in the file takes up one byte of disk space (as it contain's ASCII text. Thus, the size of the file in bytes should also be 10445. Let's confirm this:

ls -l all_data
Remember that ls -l prints out detailed information about a file and that the fifth column is the size of the file in bytes.

The awesome power of the Pipe
Suppose I wanted to only see the total number of character, words, and lines across the files Bert/* and gerdal/*4*. I don't want to see the individual counts, just the total. Of course, I could just do:

wc all_data
Since this file is a concatenation of the smaller files. Yes, this works, but I had to create the all_data file to do this. Thus, I have wasted a precious 10445 bytes of hard disk space. We can do this without creating a temporary file, but first I have to show you two more commands: head and tail. These commands print the first few, or last few, lines of a file, respectively. Try them out on all_data:

head all_data
tail all_data
The -n option to either of these commands can be used to print the first or last n lines of a file. To print the first/last line of the file use:

head -n 1 all_data
tail -n 1 all_data
Let's turn back to the problem of printing only the total number of lines in a set of files without creating any temporary files. To do this, we want to tell the shell to take the output of the wc Bert/* gerdal/*4* and send it into the tail -n 1 command. The | character (called pipe) is used for this purpose. Enter the following command:

wc Bert/* gerdal/*4* | tail -n 1
This will print only the total number of lines, characters, and words across all of these files. What is happening here? Well, tail, like many command line programs will read from the standard input when it is not given any files to operate on. In this case, it will just sit there waiting for input. That input can come from the user's keyboard or from another program. Try this:

tail -n 2
Notice that your cursor just sits there blinking. Tail is waiting for data to come in. Now type:

French
fries
are
good
then Ctrl-d. You should get the lines:

are
good
printed back at you due to you asking tail to return the last two by doing -n 2. The Ctrl-d keyboard shortcut inserts an end-of-file character. It is sort of the standard way of telling the program "I'm done entering data". The | character replaces the data from the keyboard with data from another command. You can string all sorts of commands together using the pipe.

The philosophy behind these command line programs is that none of them really do anything all that impressive. BUT when you start chaining them together, you can do some really powerful things really efficiently. If you want to be proficient at using the shell, you must learn to become proficient with the pipe and redirection operators: |, >, >>, 2> and 2>>.

A sorting example
Let's create a file with some words to sort for the next example. We want to create a file which contains the following names:

Bob
Alice
Diane
Charles
Navigate to /tmp and open an empty file with nano or notepad:

nano toBeSorted
Now enter the four names as shown above. When you are done, press Ctrl-o to write out the file. Press enter to use the file name toBeSorted. Then press Ctrl-x to exit nano (or do equivalent things in notepad).

When you are back to the command line, enter the command:

sort toBeSorted
Notice that the names are now printed in alphabetical order.

Try looking at this file with less - note that the file itself has not changed.

Short Exercise
Use the echo command and the append operator, >>, to append your name to the file, then sort it and send the output to a new file called Sorted.

Once you have looked at the new file, remove both toBeSorted and Sorted.

Let's navigate back to ~/linux_shell/shell/data. Enter the following command:

wc Bert/* | sort -k 3 -n
We are already familiar with what the first of these two commands does: it creates a list containing the number of characters, words, and lines in each file in the Bert directory. This list is then piped into the sort command, so that it can be sorted. Notice there are two options given to sort:

-k 3: Sort based on the third column
-n: Sort in numerical order as opposed to alphabetical order
Notice that the files are sorted by the number of characters.

Short Exercise
Use the man command to find out how to sort the output from wc in reverse order.

Short Exercise
Combine the wc, sort, head and tail commands so that only the wc information for the largest file is listed

Hint: To print the smallest file, use:

wc Bert/* | sort -k 3 -n | head -n 1
Putting commands into a script and execution permission [Super Useful]
Printing the smallest file seems pretty useful. We don't want to type out that long command often. Let's create a simple script, a simple program, to run this command. The program will look at all of the files in the current directory and print the information about the smallest one. Let's call the script smallest. We'll use nano or notepad to create this file. Navigate to the data directory, then:

nano smallest
Then enter the following text:

#!/bin/bash
wc * | sort -k 3 -n | head -n 1
Now, cd into the Bert directory and enter the command ../smallest. Notice that it says permission denied. This happens because we haven't told the shell that this is an executable file. If you do ls -l ../smallest, it will show you the permissions on the left of the listing.

Enter the following commands:

chmod a+x ../smallest
../smallest
The chmod command is used to modify the permissions of a file. This particular command modifies the file ../smallest by giving all users (notice the a) permission to execute (notice the x) the file. If you enter:

ls -l ../smallest
You will see that the file permissions have changed. Congratulations, you just created your first shell script!

Searching files
You can search the contents of a file using the command grep. The grep program is very powerful and useful especially when combined with other commands by using the pipe. Navigate to the Bert directory. Every data file in this directory has a line which says "Range". The range represents the smallest frequency range that can be discriminated. Lets list all of the ranges from the tests that Bert conducted:

grep Range *
Now add the --color switch:

grep --color Range *
Short Exercise
Create an executable script called smallestrange in the data directory, that is similar to the smallest script, but prints the file containing the file with the smallest Range. Use the commands grep, sort, and tail to do this.

Finding files
The find program can be used to find files based on arbitrary criteria. Navigate to the data directory and enter the following command:

find . -print
This prints the name of every file or directory, recursively, starting from the current directory. Let's exclude all of the directories:

find . -type f -print
This tells find to locate only files. Now try this command:

find . -type f -name "*1*"
The find command can acquire a list of files and perform some operation on each file. Try this command out:

find . -type f -exec grep Volume {} \;
This command finds every file starting from .. Then it searches each file for a line which contains the word "Volume". The {} refers to the name of each file. The trailing \; is used to terminate the command.

Using find like this can be slow, because it is calling a new instance of grep for each item the find returns. It's possible to use find with xargs to overcome this problem if necessary:

find . -type f -print | xargs grep Volume
find generates a list of all the files we are interested in, then we pipe them to xargs. xargs takes the items given to it and passes them as arguments to grep. xargs generally only creates a single instance of grep (or whatever program it is running).

Short Exercise
Navigate to the data directory. Use one find command to perform each of the operations listed below (except number 2, which does not require a find command):

Find any file whose name is "NOTES" within data and delete it

Create a new directory called cleaneddata (note: this should in the same directory as data)

Move all of the files within data to the cleaneddata directory

Rename all of the files to ensure that they end in .txt (note: it is ok for the file name to end in .txt.txt

Hint: If you make a mistake and need to start over just do the following:

Navigate to the shell directory

Delete the data directory with rm -r data

Enter the command: git checkout -- data You should see that the data directory has reappeared in its original state

BONUS FUN
Redo exercise 4, except rename only the files which do not already end in .txt. You will have to use the man command to figure out how to search for files which do not match a certain name.

What did we miss out? [Super Useful]
There's more we could have fitted in to this session if it were longer. Sometimes it's just useful to know that something exists so that you can research its use later. Here's a list of programs we find super useful on the command line:

awk
The Microsoft Excel of the command line. Can print elements from a row of text. Often used with grep and sed.

locate
A program which finds files in your filesystem by consulting a database.

sed
The stream editor - edit files on the fly in your scripts. Often used with awk and grep.

tail -f
The -f argument to tail "follows" a file. You can use this to watch a file grow. Often used to watch system log files.

sudo
"Super User DO". Run a command as if you were the root user of the system. For admin tasks.

ssh, scp and sftp
Network transparency. Jump from machine to machine with ssh and use it to execute commands on remote machines. Use scp and sftp to transfer files.

Regular expressions
Many programs use regular expressions, which are a more advanced version of the wild cards used by the shell. Annoyingly, there are many slightly different flavours of regular expressions, but eventually, you have to get your teeth into them (especially useful with sed and grep).

.bashrc and .bash_profile
This files are executed when the shell starts. You can put any command in there. Often used to set an alias for a long command and to set environment variables like PATH so they are correct each time you open a shell.

` characters
` characters have a special action. E.g.:

ls -l `which ls`
clear and reset
To clear your terminal, type clear. If your terminal goes all wierd, try reset.

rename
If you have lots of files to rename and you need to do it according to some pattern, then rename is your tool.

script
Allows you to log a session.

screen
Run several shells in a single terminal window in such a way that the session is immune to the network connection being lost.

Please take a look at the [Shell Cheat Sheet] (https://github.com/mikeg64/linux_shell/blob/master/shell/shell_cheatsheet.md) to refresh what you have learned and to get a quick overview of some other topics.

If you have reached this part of the document and you have time left or you would like some further practice after the workshop then please attempt the 1000 Genome Shell exercises
