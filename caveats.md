# Caveats
Adventures with the instances once setup
## Disk space
.local  
.cache
### RStudio
### Python
!pip vs pip in jupyter notebooks  
## Conda
Annaconda  
get the latest -   
https://www.anaconda.com/download - requires email  
install https://docs.anaconda.com/anaconda/install/linux/  
multiuser set up  
https://docs.anaconda.com/anaconda/install/multi-user/  

cyberduck to add to the server  
sudo bash Anaconda3-2024.06-1-Linux-x86_64.sh  
launches prompts  
install in /opt/anaconda3  
yes to everything else  
sudo groupadd conda  
sudo chgrp -R conda /opt/anaconda3/  
sudo chmod 770 -R /opt/anaconda3/  
sudo adduser <username> conda    
source /opt/anaconda3/bin/activate  
returns (base) user@computer:  
conda list  
get list of installed packages  

Gotta figure out .bashrc



