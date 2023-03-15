BASH Cheat Sheet 

2017 ICOS Big Data Summer Camp 

Most BASH commands  

- follow the pattern  $ [command] [options] [input] [output]
- tell you how to use them if you type $ [command] --help
- have a manual file with more info $ man [command]
- are explained with examples if you google them “bash [command] example” 



|**Command** |**Description** |**Quit** |**Example** |
| - | - | - | - |
|!! |Repeat the previous command. |||
|cat |Concatenate. Takes the contents of a file and puts them on the end of something else (your screen, another file, etc.) |[ctrl]+C |cat file.txt |
|cd |Change Directory. Move from one folder (directory) to another. ||cd my\_folder/data |
|cp |Copy. Make a copy of a file. See also: mv. |[ctrl]+C |cp original.html copy.html |
|diff |Difference. Print a list of all lines that are different between two files. |[ctrl]+C |diff old.csv new.csv |
|echo |Echo. Repeat whatever I type next. ||echo "Hello, World!" |
|emacs |Editor Macros. Program for editing files. Advanced users. See also: vi, nano, pico. |||
|find |Find. Search for files that match some criteria (size, date modified, name, type, and more). |[ctrl]+C |find . -name "\*.html" -size +100k |
|grep |Search for lines of text that match a pattern and print them (similar to [ctrl]+F or [cmd]+F). See also: sed. |[ctrl]+C |grep “href” kitten.html |
|head |Print just the top (head) of a file. See also: tail. |[ctrl]+C |head long\_file.txt |
|htop |Hisham Table of Processes. Like "top", but with more information and colors. |[ctrl]+C |htop |
|ll |List Long. The same as "ls -l". Will show the size, owner, date, and permissions for all files in the current directory. |[ctrl]+C |ll -h |
|ls |List files in the current directory. |[ctrl]+C |ls |
|man |Manual. Show the manual entry for a command to see how to use it and what the options are. (Use arrow keys to scroll.) |Q |man cat |
|mkdir |Make Directory. Create a new directory (folder). See also: rmdir. ||mkdir new\_folder |
|mv |Move a file or directory. See also: cp. |[ctrl]+C |mv file.txt subfolder/file.txt |
|nano |Same as "pico" but released as free software. |[ctrl]+X |nano my\_code.py |
|pico |Pine Composer. Very simple program for editing files in the terminal. See also: vi, nano, emacs. |[ctrl]+X |pico my\_code.py |
**Command**  **Description**  **Quit**  **Example** ![](Aspose.Words.64c1fe8f-9cea-448f-af36-70e5784aecec.001.png)![](Aspose.Words.64c1fe8f-9cea-448f-af36-70e5784aecec.002.png)

Print Working Directory. Show the full path of 

pwd  pwd 

what directory (folder) you are currently in. 

Remove. Deletes the specified file(s). Does not 

rm  send things to a trash folder. They are gone  [ctrl]+C  rm unwanted\_file.doc 

forever. 

Remove Directory. Deletes a specified 

rmdir  [ctrl]+C  rmdir unwanted\_directory 

directory/folder. See also: mkdir. 

Make a record of everything that I type and 

script  everything that appears in my terminal until I type  "exit" 

"exit." Then save that as a file. 

Stream Editor. The sed command can do a lot, 

sed  but it's most useful function is find and replace in  [ctrl]+C  sed 's/dog/cat/g' dog.txt > cat.txt 

text. See also: grep. 

Splits a file into multiple smaller files. See also 

split  [ctrl]+C  split big\_file.csv 

cat, which can put them back together. 

Secure Shell. Connect to a remote server's 

ssh  "exit"  ssh my.server.umich.edu 

command line. 

tail  Print just the bottom of a file. See also: head.  [ctrl]+C  tail long\_file.txt 

Table Of Processes. Shows running processes 

top  memory use. Like WIndows system monitor or  [ctrl]+C  top 

Mac activity monitor. See also: htop. 

Unix Name. Print the name and versio n of my 

uname  uname -a 

operating system. 

Visual (line editor). A program for editing files in 

vi  the terminal. Intermediate and advanced users.  [esc]+[:]+Q  vi my\_code.py 

See also: pico, nano, emacs. 

Word Count. Count many lines, words, and 

wc  [ctrl]+C  wc essay.txt 

characters are in something. 

Web Get. Download something from an internet 

wget  [ctrl]+C  wget bbc.co.uk 

URL. 

**Symbol**  **Use** ![](Aspose.Words.64c1fe8f-9cea-448f-af36-70e5784aecec.003.png)

Wildcard. Select everything. Can be combined with other characters, e.g. "\*.txt" would match all files ending in **\*** 

".txt" and "ls \*.txt" will list the files that end in ".txt". 

Overwrite. Take the output of the argument to the left and use it to replace the contents of what is on the right. E.g. "cat **>** 

updates.txt > latest.txt" will replace whatever is in 'latest.txt' with whatever is in 'updates.txt'. 

Append. Take the output of the argument to the left and add it to end end of what is on the right. E.g. "cat

**>>** 

updates.txt >> all.txt" will add whatever is in 'updates.txt' to the end of ‘all.txt' after what is already in there. 

Pipe (usually above the [enter] key). Use the output of the command to the left as input for the command to the right. **|**  E.g. in order to count the files in a directory, you can type "ls | wc -l". ls outputs a list of files, one per line. That list 

is sent ("piped") to the word count utility with the "-l" option to count lines. The result is the count of files. 

End previous command, begin a new one. E.g. “echo “We’re in”; pwd” would first print the words “We’re in” and 

**;** 

then it would print the path of the current working directory.  
