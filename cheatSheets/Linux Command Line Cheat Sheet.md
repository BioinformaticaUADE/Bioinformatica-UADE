Linux Command Line Cheat Sheet![](Aspose.Words.565de0d4-f8e1-40ff-b5f0-457d9999ba60.001.png)![](Aspose.Words.565de0d4-f8e1-40ff-b5f0-457d9999ba60.002.png)

by DaveChild

|**Bash Commands**||
| - | :- |
|uname -a|Show system and kernel|
|head -n1 /etc/issue|Show distribution|
|mount|Show mounted filesystems|
|date|Show system date|
|uptime|Show uptime|
|whoami|Show your username|
|man command|Show manual for command|


|**Bash Shortcuts**|
| - |
|CTRL-c Stop current command|
|CTRL-z Sleep program|
|CTRL-a Go to start of line|
|CTRL-e Go to end of line|
|CTRL-u Cut from start of line|
|CTRL-k Cut to end of line|
|CTRL-r Search history|
|!! Repeat last command|
|!abc Run last command starting with abc|
|!abc:p Print last command starting with abc|
|!$ Last argument of previous command|
|!\* All arguments of previous command|
|<p>^abc^123 Run previous command, replacing abc</p><p>with 123</p>|


|**Bash Variables**||
| - | :- |
|env|Show environment variables|
|echo $NAME|Output value of $NAME|
||variable|
|export|Set $NAME to value|
|NAME =value||
|$PATH|Executable search path|
|$HOME|Home directory|
|$SHELL|Current shell|


|**IO Redirection**||
| - | :- |
|command < file|Read input of command from|
||file|
|command > file|Write output of command to file|
|command >|Discard output of command|
|/dev/null||
|command >> file|Append output to file|
|command1 ||Pipe output of command1 to|
|command2|command2|
**Directory Operations![](Aspose.Words.565de0d4-f8e1-40ff-b5f0-457d9999ba60.003.png)**

pwd Show current directory mkdir dir Make directory dir

cd dir Change directory to dir cd .. Go up a directory

ls List files

 

|**ls Options**|
| - |
|-a Show all (including hidden)|
|-R Recursive list|
|-r Reverse order|
|-t Sort by last modified|
|-S Sort by file size|
|-l Long listing format|
|-1 One file per line|
|-m Comma-separated output|
|-Q Quoted output|


|**Search Files**||
| - | :- |
|grep pattern|Search for pattern in files|
|files||
|grep -i|Case insensitive search|
|grep -r|Recursive search|
|grep -v|Inverted search|
|find /dir/ -|Find files starting with name in dir|
|name name\*||
|find /dir/ -user|Find files owned by name in dir|
|name||
|find /dir/ -|Find files modifed less than num|
|mmin num|minutes ago in dir|
|whereis|Find binary / source / manual for|
|command|command|
|locate file|Find file (quick search of system|
||index)|


|**File Operations**||
| - | :- |
|touch file1|Create file1|
|cat file1|Concatenate files and output|
|file2||
|less file1|View and paginate file1|
|file file1|Get type of file1|
|cp file1 file2|Copy file1 to file2|
|mv file1 file2|Move file1 to file2|
|rm file1|Delete file1|
|head file1|Show first 10 lines of file1|
|tail file1|Show last 10 lines of file1|
|tail -f file1|Output last lines of  file1 as it|
||changes|
**Process Management![](Aspose.Words.565de0d4-f8e1-40ff-b5f0-457d9999ba60.004.png)**

ps Show snapshot of processes top Show real time processes kill pid Kill process with id pid

pkill Kill process with name name name

killall Kill all processes with names beginning name name

 

|**Nano Shortcuts**|
| - |
|**Files**|
|Ctrl-R Read file|
|Ctrl-O Save file|
|Ctrl-X Close file|
|**Cut and Paste**|
|ALT-A Start marking text|
|CTRL-K Cut marked text or line|
|CTRL-U Paste text|
|**Navigate File**|
|ALT-/ End of file|
|CTRL-A Beginning of line|
|CTRL-E End of line|
|CTRL-C Show line number|
|CTRL-\_ Go to line number|
|**Search File**|
|CTRL-W Find|
|ALT-W Find next|
|CTRL-\ Search and replace|
|More nano info at: http://www.nano-editor.org/docs.php|


|**Screen Shortcuts**|
| - |
|screen Start a screen session.|
|screen -r Resume a screen session.|
|screen - Show your current screen sessions. list|
|CTRL-A Activate commands for screen.|
|CTRL-A c Create a new instance of terminal.|
|CTRL-A n Go to the next instance of terminal.|
|CTRL-A p Go to the previous instance of terminal.|
|CTRL-A " Show current instances of terminals.|
|<p>CTRL-A A Rename the current instance of</p><p>terminal.</p>|
**File Permissions![](Aspose.Words.565de0d4-f8e1-40ff-b5f0-457d9999ba60.005.png)**

chmod 775 file Change mode of file to 775 chmod -R 600 Recursively chmod folder to 600

folder

chown Change file owner to user and user:group file group to group

**File Permission Numbers**

The first digit is the owner permission, the second the group and the third for everyone.

Calculate each of the three permission digits by adding the numeric values of the permissions below.

4 read (r)

2 write (w)

1 execute (x)
