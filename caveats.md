#Caveats
Adventures with the instances once setup
##Disk space
.local
.cache
###RStudio
###Python
!pip vs pip in jupyter notebooks
##Conda
Annaconda
get the latest - 
https://www.anaconda.com/download - require email
install https://docs.anaconda.com/anaconda/install/linux/
multiuser set up
https://docs.anaconda.com/anaconda/install/multi-user/

cyberduck to add to the server
sudo bash Anaconda3-2024.06-1-Linux-x86_64.sh
launches prompts
install in /opt/anaconda3
yes to everything else
258  sudo groupadd conda
259  sudo chgrp -R conda /opt/anaconda3/
260  sudo chmod 770 -R /opt/anaconda3/
261  sudo adduser wengang conda
262  sudo adduser todd conda
source /opt/anaconda3/bin/activate
returns (base) user@computer:
conda list
get list of installed packages

Gotta figure out .bashrc



