# CS3.301 Introduction to Linux Commands

This module introduces Linux commands to beginers. Intermediate and experts can go through this module slectively.

**TOC**
- [LESSONS](## LESSONS)
  - [Lesson 1](### Lesson 1)

## LESSONS

### Lesson 1 - Basic commands to navigate directories

Simply type

`$ pwd`

and press enter key and read on :) title: pwd

Can you see the output similar to `/home/yourname` ? cool,you have found your current working directory. Congrats,You have joined exclusive club of linux commandline users :)

As you realized typing

 `pwd`
 
will display your current working directory. Yeah,your home is a directory. Now lets try to create a new directory. Type the following on the prompt

`mkdir -v dir1`

and press enter key. title: mkdir

Did it say?

`mkdir: created directory dir1`

Wow, now you created a new directory. Lets say you want to create more than one directory instead of invoking mkdir multiple(three) times-like.

```
mkdir -v dir2
mkdir -v dir2/dir3
mkdir -v dir2/dir3/dir4
```

you can simply use

`mkdir -vp dir2/dir3/dir4`

`-p` option will create parent directories for `dir4` as needed. In this case, it creates `dir2,dir3` automatically. Now we have created 4 directories.How to view them?

To view type `ls` and press enter

`ls`

title: ls

listed `dir1 dir2` as directory content right? Thats exactly what we wanted

> __dumb tutor__: yes, the guy with blue-t-shirt, Yeah, you, why you look so confused?
> 
> __blue-t-shirt__ :I created 4 directories, where is the missing `dir3,dir4` ?
> 
> Good question.They are created inside `dir2` they won't be listed with simple command like `ls`. You need to use *complex* command to view them. Try this:

`ls -R`

really "complex" isn't it :P , btw `-R` stands for __recursive__.

Okay,we have created new directories and listed them. Now lets move into a new directory.

```
cd dir2

title: cd
```

cool,you have changed to `dir2` Now confirm this location by using previously learned pwd command. To move into next directory dir3

`cd dir3`

will place you under "dir3" directory.

**Tips and tricks**: Typing

`cd ..`
    
will move to parent directory.i.e `dir2`. Now type,

`cd -`

will move you to previous working directory i.e `dir3` Cool ,isn't it? and a simple

`cd`

will move to the your home directory.

That's it.You have successfully completed lesson1 Now to start next lesson.


Just type `vimtutor`, if you want to learn about vim text editor. If you want to change colors, please visit 'play' menu and view first screencast.

### Lesson2 - Create files, display contents and stats

During Lesson1,you have learned how to create directories.

Lets learn to create a new file,

`touch file1.txt`

and press enter key and read on :)

`title: touch`

`touch` command will create a new file or change time stamp of an existing file. Now try again,

`touch  file1.txt`

this time it will change `file1.txt` created/last access and modified time to current time.

`touch file2.txt`

will create an empty new file, if the file is not already exists. to view directory contents ,you can also use

`dir`

`title: dir`

dir is used to list directory contents. Yeah,as you guessed it correctly, `dir` is equivalent to `ls -C -b` (I know you didn't guess that :P)

that is, by default files are listed in columns, sorted vertically, and special characters are represented by backslash escape sequences. To clear a screen, the command is

`clear`
`title: clear`

Viola! terminal screen is cleared!!! Lets print some message on the terminal,

`echo "hello"`
`title: echo`

Cool! the message is displayed on the screen. Lets redirect the message to a new file instead of screen.

`echo "hello" > hello.txt`

To **append** data you must use `>>` not just `>`

```
echo "linux" >> hello.txt 
echo "world" >> hello.txt
```

Done. to view the file content, do

`cat hello.txt`
`title: cat`

so now you have viewed the file content. `cat` is used to display the entire file content.

To view only first two lines from the file

`head -2 hello.txt`
`title: head`


see, it showed us first two lines from files. By **default**, `head` will display the first 10 lines when you run,

`head hello.txt`

Now how to view last two lines?. Its simple, use `tail`

`tail -2 hello.txt`
`title: tail`

cool. Thus `head` will be used to display lines from **begining** and `tail` will be used to display **last few lines**. As with head

`tail hello.txt`

by default will display last 10 lines from the line.

Lets check some stats of the files and directories we have create so far.

`stat hello.txt`
`title: stat`

carefully examine few important fields the output. The **first line** shows the **filename**. second line says its a regular file with size as 18. Third line shows Inode number and no. of links to that inode. Fourth one,says __owner(Uid)__, __group(Gid)__ who has read-write permission but other have read permission. Final three lines show access, modified and change time. They mean:

- access - when the file was last accessed/read.
- modified - when the contents was last modified written.
- change - denotes changes to files metadata like changing user permission.

Now lets do a `stat` on directory.

`stat dir1`

Compare the previous stat "hello.txt" output with "dir1", before you move. especially find out "dir1" type. That marks the end of lesson2!. Well done!!

Now move to lesson-3.

Just type 'vimtutor', if you want to learn about vim text editor. If you want to change colors, please visit 'play' menu and view first screencast.


### Lesson3 - Copy, rename, delete files

On Lesson-1, you learned about directories. With Lesson-2, you learned about files. Now lets learn general file operations.

Now check this command

`du`
`title: du`

It displays the **disk usage** of current directory. (Please note the current total of `du` output). Use the `h` switch to output in a human readable format and the `x` switch to exclude other file systems and `~` denotes your home.

`du -xh ~`

**Tips and tricks**:

`du` can take a long time so you can specify the max. directory depth using `--max-depth` option.

`du --max-depth 3 ~`

Now lets copy `hello.txt` to `dir2` directory.

`cp -v hello.txt dir2`
`title: cp`

Now file is copied to new location. Now compute the usage again using, `du` now you should see usage has been increased by file size.

**Tips and tricks**:

`cp -v hello.txt dir2/file2.txt`

This will copy `hello.txt` into `dir2` at the same time, rename it as `file2.txt`.

`cp  -vr dir2/*.txt dir2/dir3`

This will copy all files ending with `.txt` from `dir2` into `dir2/dir3`.

`cp -vr dir2/dir3`

This will copy the directory named `dir3` to current directory.

Use `ls`, it should show you `dir3`.

Now we have copied few files, how do we verify its file integrity? simple `cat` should be enough. But If its large file or binary file, we can't use `cat`. We have to use,

`md5sum hello.txt`
`title: md5sum`

`b8d5079c5d6a9dbb3294b31d318d74c0` is the calculated checksum for a file. This helps with detecting accidental or deliberate file corruption.

When transfering a file from machine to another or downloading files from internet, to verify the file integrity compare md5sum on source and destination machines,

`md5sum dir2/hello.txt`

should be same as

`md5sum hello.txt`

now lets move to another command,

`mv hello.txt dir2/dir3/dir4/hi.txt`

will move a file into directory `dir4` and names it as `hi.txt`. so how `mv` is different from `cp`?. Try `ls` it will not show `hello.txt`.

When you use `cp` there exists two copies of a file (similar to copy-paste "ctrl-c" and "ctrl-v") with `mv` there is one copy (its cut-paste ctrl-x and ctrl-v). unlike (`cp, rm`) other commands mv don't need `-r` for directories.

create a new directory `dir5`

`mkdir dir5`

now

`mv dir2/*.txt dir5`
`mv dir5  dir50`

will move all `\*.txt` files under `dir2` into `dir5`. then rename the directory `dir5` as `dir50`.

with `mv` command we moved `hello.txt` under `dir4`, instead of accessing them as `dir2/dir3/dir4/hi.txt` everytime, we can create a link and after that, you can access or edit `dir2/dir3/dir4/hi.txt` file as simply hello

`ln  dir2/dir3/dir4/hi.txt hello`

Great! you have created a link. There are two types of links, hardlinks. where a same __inode__ pointed by two different names and softlinks which work more like shortcuts.

Hard links are created by default.

`stat hello`

and perform

`stat dir2/dir3/dir4/hi.txt`

see both uses same inode and link count shown as 2. Soft links are created using the `-s` switch.

`ln -s  dir2/dir3/dir4/hi.txt  softlink`

again do

`stat softlink`

and examine its output. New inode is created for this new symbolic link "softlink" but link count remains as 1. To remove individual file use

`rm -i file2.txt`

will prompt you with a message. `rm: remove regular empty file 'file2.txt'`? type `y` to delete the file. To remove directory, first remove it's contents using option `-r`,

`rm -ri dir50/*`

**Tips and tricks**:

If you want to remove files content without begin prompted for confirmation use `-f` option. It's **extremely dangerous** to use `rm -rf`, because you may delete very important files by mistake-so make sure you delete correct files before running `rm -rf`

`rm -rf junk/*`
`rmdir  dir50`

`rmdir` will remove an empty directory. so thats end of lesson3. Good keep going :) Time for lesson4.

Just type 'vimtutor', if you want to learn about vim text editor. If you want to change colors, please visit 'play' menu and view first screencast.

### Lesson4 - Basic process commands

In Lesson 1, you learned about directories. With Lesson 2, you learned about files. With Lesson 3, you have learned about Copying,renaming,deleting files. Now lets learn basic process-related commands.

Now check this widely used

`ps`

output is nothing but a snapshot of the currently running processes. lets create a new process.

sleep 60 &

can you see process id on screen? Now again do

`ps`

you can see the sleeping process, now-right? lets see how to stop/kill this process replace `12345` will your sleeping process id, you got above

`kill 12345`

Check again the running process list with

`ps`

sleeping process is Gone! right?

Sometimes process won't die with simple kill command, in such cases scream die!die!die! while running kill command. (hehe..just kidding) you have to use `-9` option.

`kill -9 12345`
start two process like

`sleep 30 &`
`sleep 30 &`

checking with `ps`, we can see we have two process named `sleep`, now type

`killall sleep`

did it gave an output like

`Terminated sleep 30`

right? thus `killall` terminates processes by process name.

**Tips and tricks**:

`killall -u webminal`

This kills only processes owned by user `webminal`

`killall -w find`

Wait for all `find` process to die. `killall` checks once per second if any of the killed processes still exist and only returns if none are left. Note that `killall` may wait forever if the signal was ignored, had no effect. To find a process id (`pid`) of a process you can use,

`pidof bash`

provides the process ID of a running program `bash`

**Tips and tricks**:

`pidof -s bash`

returns only one process id , instead of all process running as `bash`. You can adjust the pripority of your process by starting a process like,

`nice -n 19 sleep 30 &`

runs a program with modified scheduling priority. `nice` runs a command with an adjusted niceness, which affects process scheduling. __Nicenesses__ range from -20 (most favorable scheduling) to 19 (least favorable-the affected processes will run only when nothing else in the system wants to). Only root can increase the priority ,for example setting process nice to -20 others can lower the priority of processes they own.

how to adjust priority of currently running process with pid `12345`?

`renice -n 19 12345`

changes priority of running processes.

`renice +1 3176`

3176: old priority 0, new priority 1

`renice +4 3176`

3176: old priority 1, new priority 4

Only root can increase the priority, for example setting process nice to -20. Others can lower the priority of processes they own.

note with `renice` command, Non super-users can not increase scheduling priorities of their own processes, even if they were the ones that decreased the priorities in the first place.

To adjust priority for all process owned by a user `webminal`,

`renice +1 -u webminal`

to display running process, you can also use

`top`

see it provides a dynamic real-time view of a running system. spend sometime, examining the output. To quit from the top command, press `q`. To display commands in a tree like structure, type

`pstree`

display a tree of processes, to display `pid`, use `-p` option with pstree.

`pstree -p`

below command will let us know how long it took to complete a command.

`time ls -l`

time gives statistics about the program it ran.

- `real` - the elapsed real time between invocation and termination.
- `user` - the user CPU time .
- `sys` - the system CPU time .

Thanks, you have completed Lesson 4.

Just type 'vimtutor', if you want to learn about vim text editor. If you want to change colors, please visit 'play' menu and view first screencast.


### Lesson 5 - Manipulate or parse file contents

Lets try this widely used

`grep "linux" hello`

`grep` searches for matching words or line on the file To search entire directory of files, supply the directory name

`grep -r 'Hello'`

By default grep is case sensitive (a is not the same as A) but you can ignore case by using the `-i` switch

`grep -i 'lINUX' hello`

**Tips and tricks**:

To display line numbers:

`grep -n 'linux' hello`

To display lines that don't match the pattern:

`grep -v 'world' hello`

To count no. of words, lines and character on a file use `wc` hello title: `wc`

thus `wc` counts lines/words/bytes in a file. first field is no. of lines, second column is no.of words and third column denotes no. of bytes.

**Tips and tricks**:

`wc -L hello`

to find the length of longest line in the file. Lets create a file with some contents with echo.

`echo -e "col1 col2 r1\ncol5 col6 r2\ncol3 col4 r3 " >> new.txt`
`echo -e "Hello\nlinux\nProgrammers paradise" >> linux.txt`

Okay,you have two files new.txt, linux.txt now, lets cut it ! :D

`cut -f1 -d' ' new.txt`

So it extracted the first column from the file and to extract the third column

`cut -f3 -d' ' new.txt`

As you have noticed `-f` can be used to mention the column number and `-d` is used to specify the __delimiter__. Now we have seen how to cut a file lets check out the another one ,

`paste hello new.txt`

paste merges the lines of files

**Tips and tricks**:

to paste one file at time,

`paste -s hello new.txt`

In order to sort a file content, we could use

`sort new.txt`

File contents are sorted. Remember, we have two files `new.txt` and `linux.txt`. lets compare them

`diff hello linux.txt`


Compare files line by line. `<` denotes first file(`hello`) and `>` denotes second file(`linux.txt`). you can compare three files with

`diff3 hello new.txt linux.txt`

I'll let you to analyze the output :D we have reached end of lesson-5. move on to lesson-6.

Just type 'vimtutor', if you want to learn about vim text editor. If you want to change colors, please visit 'play' menu and view first screencast.


### Lesson 6 - Changing file attributes

Lets begin with a command that manipulates pathname,

`dirname dir2/dir3/dir4/hi.txt`

strip non-directory suffix from path name, gave you the output

`dir2/dir3/dir4`

lets use the same path with different command this time

`basename dir2/dir3/dir4/hi.txt`

this strips directory and suffix from pathname and gives the last entry.

`hi.txt`

Pretty useful commands :D lets change file access permission

`chmod -v 666 file1.txt`

You should have seen a output like mode of `file1.txt changed to 0666 (rw-rw-rw-)`

That will set the file `file1.txt` to be "world writeable". This means the owner, group and others can read and write into file. The same effect can be achived (remember you can verify it by using stat file1.txt) by

`chmod a+rw file1.txt`

where as below makes it so that no one can read or write into this file, not even it's owner!

`chmod a-rw file1.txt`

with next command only owner can read or write into this file. 

`chmod u+rw file1.txt` 

**Tips and tricks**: 

To change permission for more than one file use the `-R` switch

`chmod -R 644 ~/chmod_dir`

now to change file owner, 

`chown root file1.txt` 

`chown: changing ownership of file1.txt: Operation not permitted`

oh,thats expected error message, you can use chown only as root user, but anyway thats the syntax/usage of chown command. Now we can change file owner and group, by 

`chown root:staff file1.txt`

**Tips and tricks**:

To change permission on all files and sub-directories, use the `-R` switch.

`chown root:staff -R ~/dir2 `

Use option `--from` to change files that belongs to specific user group.

`chown --from=webminal:webminal root:staff -R ~/dir2`

will change the files the belong to `webminal` user and webminal group to root and other user files left as it is. Lets change the group alone.

`chgrp root file1.txt`

chgrp: changing group of `file1.txt`: Operation not permitted

hehe..again thats expected error message :) ,you can use chgrp only as root user, but anyway thats the syntax/usage of chgrp command.

**Tips and tricks**:

To change the group of dir2 and subfiles to "root".

`chgrp -hR root dir2`

Thats it we have completed lesson6.


### Lesson 7 - Locate file and its type

Often we need to figure out a file type,for such task, we can use

`file linux.txt`

determines the type of a file as ASCII text

`file /dev/null`

`/dev/null`: characater special says,its a character device.

**Tips and tricks**:

You can also find about file system details of special devices. (below command listed here for sake of completeness, you will get permission denied error message)

`file -s /dev/sda2`

says `/dev/sda2`: x86 boot sector, code offset 0x52, OEM-ID "NTFS ", sectors/cluster 8, reserved sectors 0, Media descriptor 0xf8, heads 255, hidden sectors 161792, dos < 4.0 BootSector (0x80)

often we need to find the location of a certain file

`whereis ls`

you should see an output

`ls: /bin/ls /usr/share/man/man1p/ls.1p.gz /usr/share/man/man1/ls.1.gz`

`whereis` command will locate source files and binaries, lets see another example, finding source file

`whereis stdio.h`

will give you

`stdio: /usr/include/stdio.h /usr/share/man/man3/stdio.3.gz`

Assume, you have installed two version a php (php4 and php5), when you simply type

`php`

which version will get executed?we don't know. In order to find it out,we use

`which php`


To locate a binary file or if you have two version of a binary file installed, you can find "which" one is currently used with this command.

Can we use which command to search for a file on a given directory? No, we can't. "which" searches only pre-defined directories shown by echo $PATH.

so in order to search a file on any directory,

`find ~ -name "linux.txt"`

Searches for files in a directory hierarchy.

**Tips and tricks**:

To find regular files and invoke the file command on the results, run

`find . -type f -exec file '{}' \;`

To find regular files and display their attributes using the ls command, run

`find . -type f -exec ls -l '{}' \;`

To find files over 20 bytes in size and list them out, run

`find ~ -type f -size +20c -exec ls -hl {} \;`

What this last command does is left as an exercise for you.

`find ~ -type f -size +20c -exec cp dir1 {} \;`

After you have practised above commands,move to our final lesson see you later.

### Lesson 8 - System and user details

Use below command to find out how long this system has been up and running,

`uptime`

uptime gives, the current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5,and 15 minutes.

To know current date and time simply use

`date`

Okay that display the current time of server running webminal.org website.

To display details about currently logged users

`who`

can you see other linux users ? :)

`who -a`

print information about users who are currently logged into the system. You can also use a single letter command,

`w`

see it gives more detailed informatio than who. `w` can display information about the users currently on the machine, and their processes.The header shows, in this order,the current time,how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes.

Displays list of mounted file system

`mount`

provides list of mounted file systems.

**Tips and tricks**:

to view only `ext4` file system,

`mount -t ext4`

to display free disk space on mounted devices.

`df -h`

`-h` switch makes the output more headable for humans. so we found `df` finds disk usage, but to find memory usage, we need to use

`free -m`

displays the total amount of free and used physical and swap memory in the system, as well as the buffers used by the kernel.

Wow!Cool,

You have completed the lesson.

### Lesson 9 - Make file 
TBD
