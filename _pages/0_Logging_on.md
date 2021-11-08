---
title: "Logging on to the cluster"
layout: archive
permalink: /logging_on/
---

Typically when working in bioinformatics we would log into a computing cluster such as the one we have prepared for this course. Those clusters provide computational resources  much more powerful than the average personal computers, allowing us to run highly complex computational tasks required by some bioinformatics analyses. When you are back in your home institutions, you can also likely use a similar method to log into the computing nodes there. How do we log in for this course? 


### Mac OS X and Linux users

#### Logging on

If you are using a Mac or Linux machine, you will need to open a `terminal` window and then type `ssh`.

`ssh` stands for [secure shell](https://en.wikipedia.org/wiki/Secure_Shell) and is a way of interacting with remote servers. You will need to log in to the cluster using both `ssh` and a keyfile that has been generated for you.

Firstly, download the keyfile and open a terminal window. Then copy it into your home directory like so:

```shell
cp mark.pem ~
```  

Give your user permission to read and write to the keyfile:  

```shell
chmod 600 mark.pem 
``` 

Then you should be able to log in with `ssh` whatever your working directory is. You need to provide `ssh` with the path to your key, which you can do with the `-i` flag. This basically points to your identity file or keyfile. For example:

```shell
ssh -i "~/mark.pem" mark@54.245.175.86
```

Of course you will need to change the log in credentials shown here (i.e. the username and keyfile name) with your own. **Also be aware that the cluster IP address will change everyday**. We will update you on this each day.

You might be prompted to accept an RSA key - if so just type yes and you will log in to the cluster!

#### Downloading and uploading files

Occassionally, we will need to shift files between the cluster and our local machines. To do this, we can use a command utility called `scp` or [secure copy](https://en.wikipedia.org/wiki/Secure_copy). It works in a similar way to `ssh`. Let's try making a dummyfile in our local home directory and then uploading it to our home directory on the cluster.

```shell
# make a file
touch test_file
# upload to cluster
scp -i "~/mark.pem" test_file mark@54.245.175.86:~/
```
Just to break this down a little we are simply copying a file, `test_file` in this case to the cluster. After the `:` symbol, we are specifying where on the cluster we are placing the file, here we use `~/` to specify the home directory.

Copying files back on to our local machine is just as straightforward. You can do that like so:

```shell
# download to local
scp -i "~/mark.pem" mark@54.245.175.86:~/test_file ./
```
Where here all we did was use `scp` with cluster address first and the location (our working directory) second - i.e. `./`

#### Making life a bit easier

If you are logging in and copying from a cluster regularly, it is sometimes good to use an `ssh` alias. Because the cluster IP address changes everyday, we will not be using these during the course. However, if you would like some information on how to set them up, see [here](https://markravinet.github.io/CEES_tips_&_tricks.html)

### Windows users

#### Logging on

If you are using a Windows machine, you will need to log on using [MobaXterm](http://mobaxterm.mobatek.net) since there is no native `ssh` client. After installing it, open MobaXterm and:

1. Start a new SSH terminal (1&2).
2. Add the host address (3) - which is the daily IP address - and your username (4) - e.g. `user2`
3. On advanced SSH settings, select "Use private key" and add the downloaded pem file (5)
4. After adding the previous informations, press "OK" to connect to the server.

![](/images/mobaxterm_tutorial.PNG)

#### Downloading and uploading files with Filezilla

Filezilla is a handy software to move files from a remote server such as the Amazon cloud or a cluster of your university.

Open Filezilla and choose Edit -> Settings.

![](/images/putty/fig10.png)

Next, choose SFTP and Add the .pem key file as indicated below and click OK.

![](/images/putty/fig11.png)

Finally, enter the IP address and the user name and when you hit enter, it should connect you. Next, time, you can use the Quickconnect dropdown menu, provided the IP address has not changed in the meantime.

![](/images/putty/fig12.png)

Now you will see the file directory system (folders) on your local computer on the left and your folders on the amazon cloud on the right. You can now just drag and drop files from one side to the other.  

#### Acknowledgements  
Although we have made some small adjustments, this *log in* tutorial was mainly prepared by Dr. Mark Ravinet and Dr. Joana I. Meier for their Physalia course on Speciation Genomics (https://www.physalia-courses.org/courses-workshops/course37/). We would like to thank both of them for allowing us to use it in this course. 
