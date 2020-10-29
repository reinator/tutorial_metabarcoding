---
title: "Linux: piping and redirection"
layout: archive
permalink: /linux_pipe/
---  

## Background  
Every program we run in the command line has three data streams connected to it, which are:  
* STDIN (0) - It is the standard input, which is the data fed into the program  
* STDOUT (1) - It is the standard output, which is the data returned by the program  
* STDERR (2) - It is the standar error, which are error messages printed out by the program. Like the STDOUT, it's printed by default to the terminal as the command executes.  

Piping and redirection are the means by which we connect these three streams between programs and files so that we can accomplish more complex tasks that demands multiple programs being execute sequentially.  

## Redirecting to a file  
By default, STDOUT and STDERR are printed in the terminal, so that the user can follow the program execution in real-time. However, there may be situations when we want to save the program output into a file, so that we can keep a record of it.  

In order to **redirect** the we need to use the operator greater than (>):  
```bash  

```
