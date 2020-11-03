---
title: "Linux: piping and redirection"
layout: archive
permalink: /linux_pipe/
---  

## Background  
Every program we run in the command line has three data streams connected to it, which are:  
* STDIN (0) - It is the standard input, which is the data fed into the program  
* STDOUT (1) - It is the standard output, which is the data returned by the program  
* STDERR (2) - It is the standard error, which are error messages printed out by the program. Like the STDOUT, it's printed by default to the terminal as the command executes.  

Piping and redirection are the means by which we connect these three streams between programs and files so that we can accomplish more complex tasks that demands multiple programs being execute sequentially.  

## Redirecting to a file  
By default, STDOUT and STDERR are printed in the terminal, so that the user can follow the program execution in real-time. However, there may be situations when we want to save the program output into a file, so that we can keep a record of it.  

In order to **redirect** the STDOUT we need to use the operator greater than (>):  
```bash  
### Creates a directory to practice piping and redirection
username@bash:~ mkdir pipe_practice  
### Moves to the recently created directory
username@bash:~/pipe_practice$
### Create empty files  
username@bash:~/pipe_practice$ touch file1.txt file2.txt file3.txt
### Running ls without redirection  
username@bash:~/pipe_practice$ ls  
file1.txt file2.txt file3.txt  
### Redirecting ls output to myoutput_1 file  
username@bash:~/pipe_practice$ ls > myoutput_1  
### Printing myoutput_1 content  
username@bash:~/pipe_practice$ cat myoutput_1  
file1.txt
file2.txt
file3.txt
myoutput_1
```
You will notice that myoutput_1 itself is also returned by the `ls` command. That's because the command line creates a file called *myoutput_1* **before** running the `ls`, so that it can later write the content returned by `ls` to *myoutput_1*. 

When redirecting to a file that does not exist yet, the command line will first create the file, then execute the command and write its output to the new file. However, when the file receiving the redirection (to the right of the `>` symbol) already exists, the redirection will **replace** the original content of the file by the content that is being redirected. If you want to keep the original content of the file and just **append** the new content to it, you rather need to use a double greater than symbol (`>>`):  
```bash  
username@bash:~/pipe_practice$ ls >> myoutput_1  
username@bash:~/pipe_practice$ cat myoutput_1
file1.txt
file2.txt
file3.txt
myoutput_1
file1.txt
file2.txt
file3.txt
myoutput_1
```
