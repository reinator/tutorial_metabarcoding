---
title: "Setting up conda"
layout: archive
permalink: /conda_setup/
---

### Conda  
Conda is ......

Since this is the first time you are running conda with your user, you need to initilize conda:

```bash 
user@bash:~$ conda init  
```  
Which should return something like this:  
```bash
no change     /home/ubuntu/miniconda3/condabin/conda
no change     /home/ubuntu/miniconda3/bin/conda
no change     /home/ubuntu/miniconda3/bin/conda-env
no change     /home/ubuntu/miniconda3/bin/activate
no change     /home/ubuntu/miniconda3/bin/deactivate
no change     /home/ubuntu/miniconda3/etc/profile.d/conda.sh
no change     /home/ubuntu/miniconda3/etc/fish/conf.d/conda.fish
no change     /home/ubuntu/miniconda3/shell/condabin/Conda.psm1
no change     /home/ubuntu/miniconda3/shell/condabin/conda-hook.ps1
no change     /home/ubuntu/miniconda3/lib/python3.7/site-packages/xontrib/conda.xsh
no change     /home/ubuntu/miniconda3/etc/profile.d/conda.csh
modified      /home/user1/.bashrc

==> For changes to take effect, close and re-open your current shell. <==
```  

Then, as conda asked you, close your session and open it again. When you open it you should see something like:
```
(base) user@bash:~$
``` 
Indicating you're in the `base` environment of conda. To activate the main conda environment for our course, where most of the programs we'll be using are installed:
```
(base) user@bash:~$ conda activate eukaryotic_genome_assembly
(eukaryotic_genome_assembly) user@bash:~$
```  

Now you are set to go :) 
