# Caveats
Adventures with the instances once setup
## Disk space
.local  

 
.cache
### RStudio
### Python
!pip vs pip in jupyter notebooks  
### caveat caveat
deleting .local will also delete the python kernal.json file, which will make the kernal throw and error. Fix by restarting the jupyterhub.service deamon. 
```
sudo systemctl stop jupyterhub.service
sudo systemctl start jupyterhub.service
```

## Conda
Tried to avoid - needed for RFDiffusion
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
## CUDA
Challenges with different versions, and GPUs -  
Software will have dependencies for specific versions. 
Needed drivers -- https://developer.nvidia.com/cuda-12-4-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local  
From history  
```
  327  apt install nvidia-cuda-toolkit
  328  sudo apt install nvidia-cuda-toolkit
  329  wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
  330  sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
  331  wget https://developer.download.nvidia.com/compute/cuda/12.4.1/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.1-550.54.15-1_amd64.deb
  332  sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.1-550.54.15-1_amd64.deb
  333  sudo cp /var/cuda-repo-ubuntu2204-12-4-local/cuda-*-keyring.gpg /usr/share/keyrings/
  334  sudo apt-get update
  335  sudo apt-get -y install cuda-toolkit-12-4
  336  sudo apt-get install -y cuda-drivers
```



