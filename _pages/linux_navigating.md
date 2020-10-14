---
title: "Linux: navigating the system"
layout: archive
permalink: /linux_navigation/
---

### Where are we?  <a name="where-are-we?"></a> 
The command **pwd** stands for *Print Working Directory* and it will print the complete path to our current directory:  
```console  
username@bash:~$ pwd  
/home/username
```  

### What's in our current directory?  <a name="what's-in-our-current-directory?"></a> 
The command **ls** will print all files and folders located in our current directory:  
```console  
username@bash:~$ ls  
Documents public_html
```  
If we want to print the content of a directory other than our current one, we need to give its path as an argument to ls:  
```  
username@bash:~$ ls /etc  
a2ps.cfg aliases alsa.d 
```  
If we want ls to print more information, we can use some of its options (remember, they will be preceded by a dash (-) symbol). For instance, option **-l** can print information on user permissions over that object, as well as its size and last modification date:  
```console  
username@bash:~$ ls -l /etc
-rwxr-xr-x  2 root root 1000000 Mar 23 13:34 a2ps.cfg
-rwxr-xr-x 18 root root 78 Feb 17 09:12 aliases
drwxr-xr-x  2 ryan users 4096 May 05 17:25 alsa.d
```  
Our last command has printed file sizes in bytes. For most cases we will want that in a human-readable format, what can be achieved by adding the **-h** option:  
```console  
username@bash:~$ ls -lh /etc
-rwxr-xr-x  2 root root 1M Mar 23 13:34 a2ps.cfg
-rwxr-xr-x 18 root root 78 Feb 17 09:12 aliases
drwxr-xr-x  2 ryan users 4,1K May 05 17:25 alsa.d
```  

If you want more information on the **ls** command (and any other command of the system), use the command **man**:  
```console  
username@bash:~$ man ls
```  
The command will print pretty useful information, such as how to execute the command, what are the options available and the arguments required (if any). 

### Moving around  <a name="moving-around"></a> 
The command **cd** (which stands for *Change Directory*) allows us to move to another directory. Its syntax is straigh-forward since it only takes one argument, which is the target directory we want to move to:  
```console  
username@bash:~$ cd Documents  
username@bash:~$ pwd  
/home/username/Documents
``` 
In the last command we used **cd** to move to the *Documents* directory, which is a subdirectory of our previous directory (*/home/username*). In this case we have typed a *relative* path to inform we wanted to move to the target directory. Another possibility could have been to inform the *absolute* path to the directory, i.e, the complete path to it:  
```console  
username@bash:~$ cd /home/username/Documents
username@bash:~$ pwd  
/home/username/Documents
``` 

### Shortcuts <a name="shortcuts"></a> 
If you want to go back to the previous (parent) directory, you don't need to specify its complete path. The shortcut **..** will do that for you:  
```console  
username@bash:~$ cd ..  
username@bash:~$ pwd  
/home/username
```  
You can even concatenate multiple **..**:  
```console    
username@bash:~$ cd ../..  
username@bash:~$ pwd  
/
```  
Now we are in the so called **root** directory. This is the top of the hierarchical structure of the system. All other directories are actually subdirectories of it.  

Another possibly useful shortcut is **~**, which represents the home directory of your user:  
```console  
username@bash:~$ cd ~  
username@bash:~$ pwd  
/home/username
```  

**Cool fact**: the shortcuts **..** and **~** also work with other commands besides **cd**:  
```console  
username@bash:~$ ls ~  
Documents public_html
```  

### The tab completion trick <a name="the-tab-completion-trick"></a>  
Typing out long paths can be tedious and slow, without mentioning the chances of typing errors (typos). However, the command line have a powerfull mechanism to help us with that: it's called **tab completion**.  

The idea is that whenever you start typing a path, if you hit the Tab key on your keyboard the command line will invoke an autocompletion action. It nothing happens, it means there are several possibilities for autocompletion. In that case you should hit Tab again to show all the possibilites, continue typing and then hit Tab again to continue the autocompletion process. Try it yourself to seed the power of tab completion!
