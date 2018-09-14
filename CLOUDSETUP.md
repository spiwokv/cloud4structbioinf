# Step by step setup of Metacentrum cloud for Structural Bioinformatics course

How to setup VM on cloud available here [CLOUDSETUP.md](https://github.com/spiwokv/cloud4structbioinf/blob/master/CLOUDSETUP.md)

1. Register to Metacentrum at:
https://metavo.metacentrum.cz/en/application/index.html (English version) or
https://metavo.metacentrum.cz/cs/application/index.html (Czech version).
Login with your UCT login and password. SOME SPECIAL INSTRUCTIONS?

2. Register to Cloud:
https://perun.metacentrum.cz/fed/registrar/?vo=meta&group=metacloud.
Login with your UCT login and password. SOME SPECIAL INSTRUCTIONS?

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
sudo apt-get update
sudo apt-get upgrade
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
sudo apt-get install gromacs
```
You can test it by typing:
```
gmx -h
```

Logout by typing `exit`. Close your virtual machine by pressing power off button in your virtual machine icon (send power off signal). Sign out from Open Nebula.



