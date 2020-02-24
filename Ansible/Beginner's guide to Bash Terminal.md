# Beginner's guide to Bash Terminal

- Bash - a Unix shell ( command line interpreter) and command language written by Brian Fox

### Linux commands

- `~` - denotes the home directory

- `ls` - what we have in the current directory.

- Add options by using `ls -<option>` command

- `pwd` - print the present working directory, i.e. where we are

- `cd <directory>` - change directory

- `cd ..` - go one level up in the directories

- `cd` - go to home directory

- `pushd <directory>` - if you need to work in a new directory while remembering the previous directory

- `popd` - takes you back to the previous directory

- `file <filename>` - tells you information on the file with the given 'filename'

- `locate <filename>` - returns everything that has that 'filename' in it

- `which <command>` - used to find out if a command is installed

- `history` - lists everything you've types in

- `whatis <command>` - gives a simple definition of the given command

- `man <command>` - the manual entry for that command

- `<command> --help` - provides help on a comman

- `touch <newfilename>` - if 'newfilename' doesn't exist, they are created

- `cp` - used to copy a file

- `mv <filename> <newfilename>` - renames/moves file 'filename' to 'newfilename'. Can overwrite a file if 'newfilename' exists

- `rm <filename>` - remove file. Cannot remove a directory

- `rm <filename>*` - removes all files in the directory or, if filename is given, all files with that filename in

- `rm -r` - removes all files and directories

- `rmdir <directoryname>` - remove a directory that has nothing in it

- `mkdir <dirname>` - makes a directory or several if several are given

- `cat <filename>` - gives the contents of a file

- `cat >> <filename>` - appends information into a file

- `cat` short for concatenate

- `cat <filename> <filename>` - puts two files together

- `more <filename>` - pages through the file

- `less <filename>` - allows navigation through a file

- `q` - quit when working with more or less

- `nano <filename>` - Allows you to text modify the file

- `cat > <filename>` - puts information in a new file

- `history | less` - shows the command history using `less`

- `ls -al / > <newfilename>` - this shows all files and directories in the home directory and writes it to the 'newfilename'

- `sudo` - allows normal user to run a command with the same privileges as the root user

- `sudo -s` - run as the root user for a certain time

- `exit` - returns to running as normal user

- `su - <username>` - change to a different user

- Not recommended to run Ubuntu as the root user

- `users` - shows who is logged into the system

- `id` - gives things like your id number etc

- Linux permissions:

  - `r` - read
  - `w` - write or delete the file
  - `x` - execute. used for files that contain code that needs to be executed

- Permissions can be given to the user, a group or everyone.

- An example of what it looks like it shown:

  ```
  -rw-r--r--
  ```

  - The first dash indicates the file type
  - the subsequent 3 (rw-) are the user permissions - read and write
  - the next 3 (r--) are the group permissions - read
  - the last 3 (r--) are everyone's permissions - read

- Each batch of three add up to 7 with r = 4, w = 2, x = 1

- To adjust permissions a number is used

- `chmod +<permission> <filename>` - adds a permission to the file

- The `<permission>` here is a number according to whether we want to read, write or execute for user, group or everyone

- For example, if I wanted the user to read and write, and the group and everyone only to read I would use '644'

- Working with a directory 755 is the same as using 644 for a file

- 'Ctrl' + 'c' - kill a command

- `killall <applicationname>` - kill any processed associated with the applicationname

### Filters

- `head [options] <path>` - prints the first 10 lines of it's input unless more lines are specified
- `tail [options] <path>` - prints the last 10 lines of it's input unless more lines are specified
- `sort [options] <path>` - sorts alphabetically the input it's given
- `nl [options] <path>` - numbers the lines in the input it's given
- `wc [options] <path>` - provides the word count, number of characters as well as lines unless specified otherwise
- `cut [options] <path>` - used to separate contents into fields (columns)
- `sed [options] <path>` - stream editor - allows us to do a search and replace on our data
- `uniq [options] <path>` - removes duplicate lines from the data. Limitation is that the lines must be adjacent to each other
- `tac [options] <path>` - performs the same as `cat` however in reverse, so the last line comes first, through to the first line last.

### Grep and Regular Expressions

- `egrep [options] <pattern> <path>` - Takes a given set of data and prints every line which contains the given pattern
- The basic building blocks of Regular Expressions are shown below
  - **.** (dot) - a single character.
  - **?** - the preceding character matches 0 or 1 times only.
  - ***** - the preceding character matches 0 or more times.
  - **+** - the preceding character matches 1 or more times.
  - **{n}** - the preceding character matches exactly n times.
  - **{n,m}** - the preceding character matches at least n times and not more than m times.
  - **[agd]** - the character is one of those included within the square brackets.
  - **[^agd]** - the character is not one of those included within the square brackets.
  - **[c-f]** - the dash within the square brackets operates as a range. In this case it means either the letters c, d, e or f.
  - **()** - allows us to group several characters to behave as one.
  - **|** (pipe symbol) - the logical OR operation.
  - **^** - matches the beginning of the line.
  - **$** - matches the end of the line.

### Piping and redirection

- Piping - the mechanism for sending data from one program to another using `|`
- Redirecting - Sometimes we want to save the output that we normally get on the screen into a file. 

- `\>` - Save output to a file.
- `\>>` - Append output to a file.
- `<` - Read input from a file.
- `2>` - Redirect error messages.
- `|` - Send the output from one program as input to another program.

### Process Management

- `top` - Gives a snapshot of what is currently running
  - **Line 2** Tasks is just another name for processes. It's typical to have quite a few processes running on your system at any given time. Most of them will be system processes. Many of them will typically be sleeping. This is ok. It just means they are waiting until a particular event occurs, which they will then act upon.
  - **Line 3** This is a breakdown of working memory (RAM). Don't worry if a large amount of your memory is used. Linux keeps recently used programs in memory to speed up performance if they are run again. If another process needs that memory, they can easily be cleared to accommodate this.
  - **Line 4** This is a breakdown of Virtual memory on your system. If a large amount of this is in use, you may want to consider increasing it's size. For most people with most modern systems having gigabytes of RAM you shouldn't experience any issues here.
  - **Lines 6 - 10** Finally is a listing of the most resource intensive processes on the system (in order of resource usage). This list will update in real time and so is interesting to watch to get an idea of what is happening on your system. The two important columns to consider are memory and CPU usage. If either of these is high for a particular process over a period of time, it may be worth looking into why this is so. The USER column shows who owns the process and the PID column identifies a process's Process ID which is a unique identifier for that process.
- `ps` - another way to look at the processes
- `kill <processID>` - kills the selected process
- `sleep <seconds>` - waits for a given number of seconds and then quits
- `jobs` - lists the current background jobs
- `fg <jobnumber>` - brings background processes into the foreground
- 'Ctrl' + 'z' - Pause the current foreground process and move it into the background

- `htop` - nicer version of `top`

