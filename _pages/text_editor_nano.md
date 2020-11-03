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
* The **second line** is where your file content begins. You can easily change its content by directly writing or deleting content. Notice that in this example *nano_file1.txt* is empty since we have just created it.
* Finally, the **last line** shows some shortcuts that you will probably want to use while editing your file.  

### Editing the file  
The process of putting data into the file is pretty straightforward. You just need to type the text you want to include. The `↵ Return` key will skip to the next line. And to delete text, just do like in any other text editor, using either backspace (←) or delete (DEL) keys. To navigate across the file, you can use the arrow keys (↑ ↓ ← →). 

You can play around and add any text you want to:  
![](/images/nano_02.PNG) 

### Saving the changes  
To save the changes that you have made to the file, use the shortcut Ctrl+O (always lower case!). Nano will ask the name you want to give to the modified version of the file. If you want to keep the original file name, just press the `↵ Return` key.  
![](/images/nano_03.PNG)  

After saving the modified version, Nano will return to the first page. If you want to leave Nano, you need to use the shortcut Ctrl+X. 

PS: If any modifications have been done between the last save action and the moment you try to leave Nano, it will ask you if you want to save the modifications into a new file. 
