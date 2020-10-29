---
title: "Linux: pattern searching"
layout: archive
permalink: /linux_pattern_searching/
---  

## Wildcards  
The command line is capable of understanding patterns of strings (which we will call here *wildcards*), which allows us to simultaneously run commands for multiple files/directories using only a few characters.  

### The `*` wildcard

The most frequently used wildcard is `*`, which represents zero or more characters. Let's see how it works with a real example:  

First create a folder named `wildcards_test` and move to it:
```bash  
username@bash:~$ mkdir wildcards_test
username@bash:~$ cd wildcards_test
```

Now create five empty files:  
```bash  
username@bash:~/wildcards_test$ touch carol.txt blah.txt example.png firstfile.txt number2file 
```  

Now we can use the wildcard `*` to list only the files that begin with the letter *b*:  
```bash  
username@bash:~/wildcards_test$ ls b*  
blah.txt
```

What if we wanted to list all the files that end with *.txt*?  
```bash  
username@bash:~/wildcards_test$ ls *.txt  
carol.txt  blah.txt  firstfile.txt 
```

### Under the hood  
What is happening under the hood is that first the command line will process the wildcard and return the files/directories that match with it. Then it will pass all those files/directories as arguments to the command that is being executed. In the above example we have run the command `ls`, however wildcards will work with any other command.  

For instance, imagine we wanted to create a folder called *images* and move all files with *PNG* extension to it. We can do that by combining the wildcard `*` with the command `mv`:  
```bash  
username@bash:~/wildcards_test$ mkdir images  
username@bash:~/wildcards_test$ mv *.png images/  
username@bash:~/wildcards_test$ ls images/ 
example.png
```

### The `?` wildcard  
The `?` wildcard represents a single character. For example, it can be used to list all files whose second letter is *a*:  
```bash  
username@bash:~/wildcards_test$ ls ?a*   
carol.txt
``` 
Or even to list all files whose extension have three characters:  
```bash  
username@bash:~/wildcards_test$ ls *.???   
carol.txt blah.txt firstfile.txt
```  

### The `[]` wildcard 
Finally, as opposed to `*` and `?`, which refer to **any** character, the range operator `[]` allows us to search for a specific subset of characters.  

For instance, if we wanted to list all files that begin the the letter *c* or *f*:  
```bash  
username@bash:~/wildcards_test$ ls [cf]*   
carol.txt firstfile.txt
``` 

Or to list all files that contain a numeric character:  
```bash  
username@bash:~/wildcards_test$ ls *[0-9]*   
number2file
``` 
