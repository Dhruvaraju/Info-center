# Linux
## bin
Contains binaries for basic operation like ls, cat

## sbin
Contains system binaries, standard user do not access to this with out permission
like apt. Where you need to be a root or super user.

 > Single user mode needs these folders to be perform system repairs or updates.

## boot
Boot loaders will live here, anything related to booting will be present here.

## dev
Every device is considered as file and stored here. Every device will have a file here. Generally partitions are stored as sda, sda1 .,

## etc
All configurations are present like apt configuration. Configurations for system wide apps will reside here not user specific apps.

## lib folders
lib, lib32, lib64 contains files that are required for apps to perform their operations.

## mnt
where the devices or storage is mounted.

## opt
Manually installed vendor software reside here. 

## proc
Information on all processes are present here.

## root
Is root user's home directory.

## run
Temporary file system, generally ram processes uses this.

## srv
When running linux in server mode the files that need to be hosted are placed in this folder.
Web server related files will also be stored here.

## sys
A way to interact with kernel, created every time system reboots.

## tmp
temporary files are present like browser history and app temp folders.

## usr
Used for storing user installed applications, many apps installed will have all their folders across sub folders in the folder.

## var
Files and directories that grows in size will be placed. Like mail database.

## home
Each user will have their own folder. Users will stores all their information in this folder.