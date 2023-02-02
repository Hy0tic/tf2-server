# tf2-server
[original instructions](https://aarmastah.xyz/misc/tf2vps.php)

# Setup Linux environment
Login as root user  
Run:
```
useradd tfds
```
Run ```passwd tfds``` to set new password for user tfds  

Run:
```
usermod -aG sudo tfds
sudo usermod --shell /bin/bash tfds
sudo mkdir /home/tfds
sudo chown tfds /home/tfds
sudo apt update
sudo apt upgrade -y
```

# Install SteamCMD and TF2 Dedicated Server
```
sudo mkdir /hlserver
sudo chmod 775 /hlserver
sudo chown tfds /hlserver
cd /hlserver
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install lib32z1 libncurses5:i386 libbz2-1.0:i386 lib32gcc-s1 lib32stdc++6 libtinfo5:i386 libcurl3-gnutls:i386 libsdl2-2.0-0:i386 -y
wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
tar zxf steamcmd_linux.tar.gz
nano tf2_ds.txt
```
Paste this into ```tf2_ds.txt```: 
``` 
login anonymous
force_install_dir /hlserver/tf2
app_update 232250
quit
```
Press Ctrl + X, then Y, then Enter.
Run:
```
nano update.sh
```
paste this into ```update.sh```:
```
./steamcmd.sh +runscript tf2_ds.txt
```
Press Ctrl + X, then Y, then Enter.  
Run: 
```
sudo chmod +x steamcmd.sh update.sh
sh update.sh
```

# Testing TF2 Dedicated Server
Run 
```
nano tf.sh
```
Paste this into ```tf.sh```:
```
#!/bin/sh
tf2/srcds_run -console -game tf -timeout 0 -autoupdate -steam_dir /hlserver -steamcmd_script /hlserver/tf2_ds.txt +maxplayers 24 +map ctf_2fort +sv_pure 0
```
Press Ctrl + X, then Y, then Enter.

Run: 
```
sudo chmod +x tf.sh
sh tf.sh
```
Open Team Fortress 2 on your client computer and enter the console command ```connect [server's IP]```

# Additional Setup and Customization
```
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 27015
sudo ufw enable
```
Connect to the server using Firezilla, go to ```hlserver/tf2/tf/cfg```
Generate server cfg [here](https://avi12.com/tf2-server-cfg-generator), then paste it into the ```cfg``` folder
