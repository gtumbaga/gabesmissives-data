# Mount an FTP Server as a Drive in Ubuntu
---
I do sidework for a company, that for certain reasons, I am unable to git clone a local copy of the site.  So when I do work on their site, I need to FTP in.  However, my editor of choice is VIM.  Until today, I was using filezilla to connect to their FTP, and using the rightclick > View/Edit in order to open a local copy of the file, and was using VIM locally to edit the file, then going back to filezilla (that is listening for changes) and clicking ok to let it upload the modified file.

I know that VIM actually does have the ability to connect and browse an FTP, but for some reason with this FTP server it was not working.  So today, I found a way to mount an FTP server as a drive in Ubuntu, using a utility named `curlftpfs`.


## Installation
Installation was pretty simple, using apt-get:
```
sudo apt-get install curlftpfs
```

## Connection
1. Create a directory to mount.  I personally used `~/mnt/directoryname/`
```
mkdir ~/mnt/directoryname
```

2. My password for this FTP had special characters in it, so I had to use a special switch to be able to quote my username and password:
```
curlftpfs -o user='username:passwordwithspecialcharacters' thefptserver.com ~/mnt/directoryname/
```

3.  From here, I was able to browse ~/mnt/directoryname as a directory, and can use `VIM .` to browse it as though its local.


## Umount
It's proably not secure to leave an FTP server mounted, so you can unmount when you're done:
```
sudo umount ~/mnt/directoryname
```

## That's It!
This made my workflow for this particular situation waaaaaaay better than the filezilla solution!


---
sources:
- https://linuxconfig.org/mount-remote-ftp-directory-host-locally-into-linux-filesystem
- https://stackoverflow.com/questions/8959905/linux-curlftpfs-password-with-symbols
