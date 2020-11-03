---
title: "Nano"
layout: archive
permalink: /nano/
---  

In the last section you have created empty files using the command `touch`. Now, let's learn how to put content into files using the popular text editor **nano**.  

```bash  
### Creates a directory to practice piping and redirection
username@bash:~$ mkdir nano_practice  
### Moves to the recently created directory
username@bash:~$ cd nano_practice  
### Creates a new file called nano_file1.txt and opens it with nano  
username@bash:~$ nano nano_file1.txt
```

When you create a file using **nano**, you will see the following home page: 

![](/images/nano_01.PNG)  

* The **first line** shows the version of the nano editor you are using (in this example, version 2.2.6) as well as the name of the file that is being edited.  
* The **second 2** is where your file content begins. You can easily change its content by directly writing or deleting content. Notice that in this example *nano_file1.txt* is empty since we have just created it.
* Finally, the **last line** shows some shortcuts that you will probably want to use while editing your file.  
