---  
title: "Linux: file manipulation"  
layout: archive 
permalink: /linux_file_manipulation/
---  

# 3. File manipulation <a name="file-manipulation"></a>  
## 3.1 Creating a directory <a name="creating-a-directory"></a>  
You can create a directory inside your current directory using the command **mkdir** (which stands for *Make Directory*):  
```console  
username@bash:~$ mkdir linux_tutorial 
username@bash:~$ ls  
Documents linux_tutorial public_html
```  
The execution above has created a directory inside our current working directory, which was */home/username*. However we can use **mkdir** to create a directory in any other location. Let's suppose we wanted to create a directory in the Documents directory instead:  
```console  
username@bash:~$ mkdir Documents/linux_tutorial_2 
username@bash:~$ ls  
Documents linux_tutorial public_html  
username@bash:~$ ls Documents  
linux_tutorial_2
```  
We can also create directories using absolute paths:  
```console  
username@bash:~$ mkdir /home/username/Documents/linux_tutorial_3 
username@bash:~$ ls Documents  
linux_tutorial_2 linux_tutorial_3
```  
## 3.2 Creating a file <a name="creating-a-file"></a> 
We can use the command **touch** to create an empty file:  
```console  
username@bash:~$ touch empty_file 
username@bash:~$ ls   
Documents empty_file linux_tutorial public_html
``` 
Do not worry: later on in this tutorial you will learn how to put data into the files you have created.  

## 3.3 Copying a file <a name="copying-a-file"></a>  
There are several reasons why you may want to copy a file, for instance when you want to create a backup copy before modifying the original copy. The command to create copies is **cp**. It takes two arguments: the first one is the file to be copied (i.e. the source) and the second is the destination. 

The destination is a path to either a file or a directory. If destination is a directory, then the **cp** command will create a copy of the source file in the destination directory and keep the original filename of the source file:  
```console  
username@bash:~$ cp empty_file linux_tutorial 
username@bash:~$ ls linux_tutorial  
empty_file
``` 
However, if the destination is a file, the **cp** command will create a copy of the source file with the new filename specified. This will be necessary when you want the copied file to have a different name:    
```console  
username@bash:~$ cp empty_file linux_tutorial/empty_file_backup 
username@bash:~$ ls linux_tutorial  
empty_file empty_file_backup
```  

## 3.4 Copying a directory <a name="copying-a-directory"></a>  
We will use the same **cp** command to copy an entire directory, however now we need to specify the *-r* option, which will indicate we want to copy the source directory and all of its files and subdirectories:  
```console  
username@bash:~$ cp -r linux_tutorial linux_tutorial_backup 
username@bash:~$ ls   
Documents empty_file linux_tutorial linux_tutorial_backup public_html  
username@bash:~$ ls linux_tutorial_backup  
empty_file empty_file_backup
```  

## 3.5 Moving files and directories <a name="moving-files-and-directories"></a>  
The command to move a file or directory from one directory to another is **mv** (which stands for *Move*).**mv** works in similar way as **cp**, where the first argument is the source and the second one is the destination. One advantage of **mv** over **cp** is that **mv** do not need the option *-r* to move directories, so the command is actually the same either you want to move a file or a directory:  
```console  
username@bash:~$ mv linux_tutorial/empty_file Documents
username@bash:~$ ls Documents  
empty_file linux_tutorial_2 linux_tutorial_3 
username@bash:~$ ls linux_tutorial  
empty_file_backup
```  
So in the command above we have moved the file *empty_file* from the *linux_tutorial* to the *Documents* directory.  

## 3.6 Renaming files and directories <a name="renaming-files-and-directories"></a>  
The command **mv** can also be used to rename a file or directory. This is accomplished when the source and destination directories are the same:  
```console  
username@bash:~$ ls linux_tutorial
empty_file_backup  
username@bash:~$ mv linux_tutorial/empty_file_backup linux_tutorial/empty_file_backup_renamed 
username@bash:~$ ls linux_tutorial  
empty_file_backup_renamed
```  
```console  
username@bash:~$ ls  
Documents empty_file linux_tutorial linux_tutorial_backup public_html
username@bash:~$ mv public_html public_html_renamed 
username@bash:~$ ls  
Documents empty_file linux_tutorial linux_tutorial_backup public_html_renamed
```  
In the first example, the file *empty_file_backup*, inside the directory *linux_tutorial*, is renamed to *empty_file_backup_renamed*.  
In the second example, the directory *public_html*, inside our current directory, is renamed to *public_html_renamed*.

## 3.7 Removing a file <a name="removing-a-file"></a>  
The command to remove a file is **rm**, which stands for *Remove*. The only argument it takes is the path to the file to be removed:  
```console  
username@bash:~$ ls linux_tutorial_backup  
empty_file empty_file_backup 
username@bash:~$ rm linux_tutorial/empty_file_backup  
username@bash:~$ ls linux_tutorial_backup  
empty_file
```  

## 3.8 Removing a directory <a name="removing-a-directory"></a> 
The command **rm** can also be used to remove entire directories, however just like for the command **cp**, we need to add the *-r* option:  
```console  
username@bash:~$ ls  
Documents empty_file linux_tutorial linux_tutorial_backup public_html
username@bash:~$ rm -r linux_tutorial_backup 
username@bash:~$ ls  
Documents empty_file linux_tutorial public_html_renamed
``` 

### Attention :grey_exclamation: 
Since Linux command line does **not** have an **undo** option, be **careful** when performing **destructive** actions. 

# Additional references <a name="additional-references"></a>  
This tutorial was inspired by the great [Ryan Chadwick's webpage](https://ryanstutorials.net/linuxtutorial/) on Linux. If you want to deepen your understanding on Linux, I highly recommend you to browse through Ryan's tutorial, which includes exercises and some other interesting topics not coverede here due to time constraints.
