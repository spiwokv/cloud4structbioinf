# Using Metacentrum cloud for Structural Bioinformatics course

How to setup virtual machine in cloud available here [CLOUDSETUP.md](https://github.com/spiwokv/cloud4structbioinf/blob/master/CLOUDSETUP.md)

1. Open Putty and enter an address *your_login*`@`*IP_address*. Your login and IP address will be given to you at
the first lesson. Type password when asked (password does not show on the screen while typing!!!). The password will
be given to you.

2. Change password. Type:
```
passwd
```
You will be asked for old password, new password and new password again.

3. Modify `.bashrc` file so that Midnight Commander stays in the directory when closed. Open Midnight Commander
by typing:
```
mc
```
Press F9 and go to Options > Configurations and switch on 'Use Internal Edit' using Space tab.

Next, in your home go to file `.bashrc`, pres F4 to edit, go to the end of file and add line:
```
alias mc=". /usr/share/mc/bin/mc-wrapper.sh"
```
Save by F2 and close by F10. Close Midnight Commander by F10.

4. Exit by typing:
```
exit
```

