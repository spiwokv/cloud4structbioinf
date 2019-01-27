# Step by step setup of Metacentrum cloud for Structural Bioinformatics course

1. Register to Metacentrum at:
https://metavo.metacentrum.cz/en/application/index.html (English version) or
https://metavo.metacentrum.cz/cs/application/index.html (Czech version).
Login with your UCT login and password.

2. Register to Cloud:
https://perun.metacentrum.cz/fed/registrar/?vo=meta&group=metacloud.
Login with your UCT login and password.

3. Prepare your access key:
- Download puttygen.exe from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html (chose correct version, either 32 of 64 bit)
- Run puttygen.exe (no installation necessary), set type to RSA and press 'Generate'. Now move randomly by mouse over the window. The program uses the randomness of mouse motions to generate the key. Your key appears in the the window "Public key for ...". It starts with "SSH-RSA ", followed by a long series of numbers and letters. Save the key pair by pressing "Save private key" and "Save public key".

4. Load keys into Putty.

5. Open http://cloud.metacentrum.cz/ and log in. Click to your login in right top corner and click to Settings. Click to "Update SSH key" and add your public key.

6. Click to VM icon. To create a new virtual machine click to "+" icon. Give some simple name to your virtual machine. Select
- image: CERIT-SC-Debian 9
- settings: 2 GB RAM, 1 CPU, 1 VCPU, disk 0: 10 GB, disk 1: 8 GB
- networks: cerit-sc-cloud-private1 + cerit-sc-cloud-public253

Start your virtual machine.

7. In your virtual machine icon you will see its IP address starting 147. Open Putty and connect to address root@IP_address (e.g. root@147.251.255.43).

8. If your login was successful, update and upgrade software by typing:
```
apt update
apt upgrade # press y when asked
```
make a new directory by typing:
```
mkdir install
```
Go to this directory by typing:
```
cd install
```
and install Modeller by typing:
```
wget https://salilab.org/modeller/9.20/modeller_9.20-1_amd64.deb
env KEY_MODELLER=XXXXXX dpkg -i modeller_9.20-1_amd64.deb 
```
(replace XXXXXX by a correct Modeller key given by the tutor). You can test it by opening python and typing `import modeller`. No output means correct installation. Close python by typing Ctrl+D.

Install Gromacs by typing:
```
apt update
apt upgrade # press y when asked
apt install gromacs # press y when asked
```
You may skip the first two lines if you install Gromacs immediatelly after Modeller. You can test it by typing:
```
gmx -h
```

Install R by typing:
```
apt update
apt upgrade # press y when asked
apt install r-base # press y when asked
```
You can try by typing:
```
R
```
(type `q()` and select `n` to exit).

To install PoVRay type:
```
apt update
apt upgrade # press y when asked
apt install git # press y when asked
apt install autoconf # press y when asked
apt install libboost-thread-dev # press y when asked
apt install libtiff-dev # press y when asked
cd ~/install
mkdir povray
cd povray
git clone https://github.com/POV-Ray/povray.git 
cd povray/unix/
./prebuild.sh
cd ..
./configure COMPILED_BY="your e-mail"
make
make install
```
Replace "your e-mail" by your e-mail. You can try by typing:
```
povray -h
```

To install Mplayer type:
```
apt update
apt upgrade # press y when asked
apt install yasm # press y when asked
cd ~/install
mkdir mplayer
cd mplayer
wget http://www.mplayerhq.hu/MPlayer/releases/mplayer-export-snapshot.tar.bz2
tar xvjf mplayer-export-snapshot.tar.bz2
cd mplayer-export-2019-01-25 # <-replace by correct date
./configure # press enter when asked
make
make install
````
You can test by typing:
```
mplayer
```

To install Gromacs patched by Plumed, compile Plumed, patch Gromacs by Plumed and compile Gromacs:
```
apt update
apt upgrade # press y when asked
apt install cmake # press y when asked
apt install fftw3 fftw3-dev # press y when asked
cd ~/install
mkdir plumed
cd plumed/
git clone https://github.com/plumed/plumed2.git
cd plumed2/
make
make install
cd ..
mkdir gromacs
wget http://ftp.gromacs.org/pub/gromacs/gromacs-2018.4.tar.gz
tar -xvzf gromacs-2018.4.tar.gz 
cd gromacs-2018.4
plumed patch -p
mkdir build
cd build
cmake .. -DGMX_DEFAULT_SUFFIX=OFF -DGMX_BINARY_SUFFIX="_plumed"
make
make install
```
You can test by typing:
```
/usr/local/gromacs/bin/gmx_plumed -h
```

Logout by typing `exit`. Close your virtual machine by pressing power off button in your virtual machine icon
(send power off signal). Sign out from Open Nebula.



