Knowing your way around Linux is an essential skill in CTFs, as there are many useful tools for CTFs available for 
Linux environments - some exclusive to Linux. It can be a little daunting at first, but this guide will
get you running in no time!

Linux is not an Operating System on its own, rather it is the piece of software that allows for the hardware and the
software processes to communicate with each other (this is formally known as a kernel). It is therefore the basis 
upon which people can build their own Operating Systems. Because of this, there are many Linux distributions 
available online, think of them as Linux 'flavours' that come bundled with pieces of software to suit a specific set 
of needs. Some general-purpose distributions - often shortened as distros - are Ubuntu, Linux Mint and Fedora, for 
example, which feature similar desktop environments to what you find in Windows. Moreover, you can try them out from 
your Windows environments thanks to 
![WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install) (Windows Subsystem for Linux).
For our purposes, we recommend using [Kali Linux](https://www.kali.org/get-kali/), formerly BackTrack Linux, which 
features a lot of the tools you will need during your CTF adventures and is also compatible with WSL 2. Without 
further ado, let's get started!

### Meet your new best friend: the terminal!
Despite having a desktop to work with, it's about time we get familiar with the terminal (known as command prompt
in Windows), since most tools won't have a GUI (Graphical User Interface) and will have to be run from the
terminal instead, which will most likely be the terminal we know as **bash**. Once you open the terminal, you will 
find the following: 

!["Linux terminal"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_cmd.png?raw=true "Linux terminal")

It is here that you can type your commands. We recommend you follow along with this guide to get some practice
going, which is the best way to learn.

### Directories and file structure
Whenever you open the terminal you will be put into your home directory. In order to check which directory we are
in we can use the `pwd` (Print Working Directory) command.

!["Output of the pwd command"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_pwd.png?raw=true "Output of the pwd command")

As you can see, in this example the current directory is `/home/john.doe`. What does this mean? It's time we talked
file structures! Most Linux-based OS have the same file structure, which has the root of the filesystem represented
by `/`. Often times we look at filesystem as trees we go up and down in, so this would be the top level. In order
to explore this, we can use the `ls` (List) command. If we type it on its own it lists the contents of the current
directory, but some commands accept what we know as arguments and if we provide a path to `ls` it will instead list
the contents of the specified directory. In the following example, `/` is an argument we pass onto `ls`:

!["Listing contents of root directory"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_ls.png?raw=true "Listing contents of root directory")

You will see a variety of folders, which some distros will represent with a blue colour. If you remember the previous
example, you might spot that there's a `home` folder here. Indeed, that is what `/home/john.doe` means: from the root
go into the `home` folder and then into the `john.doe` folder! But how do we actually go into the folder? In order to 
do this we have to use the `cd` (Change Directory) command:

!["Changing directories with cd"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_cd.png?raw=true "Changing directories with cd")

As you can see the argument in this case is the path of the directory we want to move to. If we provide no arguments
then `cd` will land us in our home directory, which in **bash** can also be referenced as `~`. Each user has their own
home directory, usually under a folder of their name in `/home/`. Finally, the current directory can also be referenced 
as `.` and we can use `..` to reference the level above the current one (the previous folder). Remember these symbols 
as they will come quite useful to optimise your workflow.

Terminal environments are different from desktop environments in that you do not need to be in a directory in order to
create, delete, edit or execute the files inside it. If I mention a file such as `script.py` on its own, then the
terminal will think it's a file located in the current directory. This is known as a **relative path** and in this case
it would be interpreted as `./script.py` (remember how `.` represents the current directory!). However, we can also
provide an **absolute path**, which is the path starting from the root. In our example this could look something like
`/home/john.doe/script.py` and in this case the Bash terminal doesn't care where we are, since it has the full directions
to retrieve the file anyway.

So far we have been traversing directories, but we can also create them! The `mkdir` (Make Directory) command is our 
friend here and can be used to create a new directory or series of directories, each separated by a space (remember 
you can use relative paths to create them in the current directory or absolute paths to choose exactly where to create 
the folders):

!["Creating directories with mkdir"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_mkdir.png?raw=true "Creating directories with mkdir")

### A small note on command options 

Before moving on to how to create files, let's introduce the concept of options (or flags). Some commands offer
additional functionality we can enable and disable to suit our needs. A perfect example of this is `ls`. We will be
adding the following options to it (notice how options are usually indicated by a single or double dash `-`/`--`:
- `-l`: display the result in the **long listing** format, also including file attributes and permissions.
- `-a`: lists **all** contents, including hidden files and folders.
- `-h`: changes file sizes to be displayed in **human-readable**  sizes (1K 243M 2G).
The result of running the command with these options results in the following output:

!["Using ls with options"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_ls_options.png?raw=true "Using ls with options")

We'll explore what all of this means shortly, but if you ever want to know what flags a command supports, you can use the
`man` command to find out, passing the command you want to know more about as an argument to it.

### File creation, edition and execution (now permission-flavoured!)

In the same way we could create folders using the `mkdir` command, we can do the same with files using the `touch` command, 
which creates a new blank file ready for you to edit. As an example, let's try creating a Bash script that prints "Hello" 
to the terminal using `touch my_script`. Now we have to edit it, which can be done using any text editor. While you can you 
whatever you feel comfortable with, some common command-line editors are **nano** and **vim**, which can be used with 
`nano my_script` and `vim my_script` respectively, assuming they are installed in your system (if not you can install them 
by using the `apt install <package_name>` syntax). Write the following into it (in vim you'll have to press `i` to enter 
INSERT MODE so you can type normally):
```bash
#!/bin/bash
echo "Hello"
```
The first line tells the Bash what to open the file with (in this case bash itself, now you know where its binary lies!) and
the second line is the `echo` command, which prints whatever is passed to it as an argument to the terminal. Now you can save
the file by pressing `Ctrl+X` on nano or by pressing `ESC` and then typing `:wq` to instruct it to write the changes and quit.
With this, our file is created! We can check whether it has been saved correclty by checking its contents. To do so we could
open the file again in an editor, but this time we'll introduce the `cat` (Concatenate) command, which reads data from a file
and gives its content as an output. In this instance the full command would be `cat my_script`. This approach works fine in this
case because the file is short, but for longer files it may be troublesome as all the contents are printed at once, so we would
have to scroll a lot. When we find ourselves in those cases, the `less` command may come handy, as it displays the contents one
page at a time and we just have to press the spacebar to move pages (pressing the `q` key closes less and goes back to the prompt).

Now there is one step left, which is to make the file executable. By default, files are not executable and you have to make them 
so by using the `chmod` (Change Mode) command:

```bash
chmod +x my_script
```

This basically adds the executable (+x) flag to the file so it can be run. This ties back to the `ls -lah` command, where we
can check this flags:

!["Using ls with options"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_ls_options_2.png?raw=true "Using ls with options")

Here you can see that for every entry listed the first flag indicates whether it's a directory and then there are 3 groups of
3 letters each, which indicate whether that group can read/write/execute (r/w/x) the file (folders need execution permissions). Here is
a basic table to understand it with the file `my_script` as an example:

| User         | Group     | Other |
|--------------|-----------|-------|
| rwx          | r-x       | r-x   |

User refers to the owner of the file, indicated by the first name in the line of the `ls -lah` output. In this case the owner is
`root`. Group refers to the owning group for the file, indicated by the second name in the line of the output, which in this case is
also `root`. By default users have a group created with their same name that they automatically belong to and `root` is the highest
privileged user in the system (you can check your user with the `whoami` command). Finally, Other refers to users that aren't the
owning user and that do not belong to the owning group. When a letter is replaced by a dash, it means that permission is not present.
The `chmod` command we executed earlier just added the executable mode to User, Group and Other at the same time, and we can get the
same resulting modes by using the full-fledged command `chmod u=rwx,g=rx,o=rx my_script`. You can also use the `chown` command to change
the owning user and group, but you may need elevated permissions to do so if you are not the owner of the file.

As the final step, you can run the script we have created by referencing it with `./my_script`, like so:

!["Running a Bash script"](https://github.com/Vintrae/How-To-CTF/blob/main/images/linux_script.png?raw=true "Running a Bash script")

It works!

### The graveyard of commands I couldn't place elsewhere.

To end this guide there are 4 quick commands left to cover. Some of them I couldn't mention earlier and some I just forgot! The commands
are the following:
- `mv` (Move): can be used to move the file specified by the first argument to the location specified by the second one. This can also
be used to rename a file by moving it to the same location but giving it a different name.
- `cp` (Copy): can be used to copy the file specified by the first argument to a different location, or to the same location under a
different name.
- `rm` (Remove): can be used to delete a file or group of files.
- `clear`: the command you've probably been waiting for the entire guide! This command will empty the screen and leave you with a clean
prompt to continue your work.

That's it! This will do for the introductory guide. Hope this will give you the basics you need to navigate Linux-based systems and know
your way around. 




