# Linux

## Find occupied IPs on the network

You'll need _nmap_ for this

    sudo snap install nmap

Once installed, you can find all the hosts that respond to ping requests on the
network (IP addresses ranging between 192.168.1.0 to 192.168.1.255) by typing
the following:

    nmap -sn 192.168.1.0/24

## Increase sudo password timeout
If you like to increase timeout of sudo session in terminal, to say 4 hours,
type:

    sudo visudo

then add the following line:

    Defaults        env_reset, timestamp_timeout=240

## Difference between binary files
    cmp -l file1.bin file2.bin

## Disk usage from current directory
    du -sh *

## Disk usage per partition
    df -h
    
## Print end of file and follow file updates
    tail -f temp.log


# Windows

## Delete directories (including subdirectories and files

Navigate into the directory you want to remove (e.g. _foldername_)

    DEL /F/Q/S *
    CD ..
    RMDIR _foldername_ /Q/S

## Get rid of windows installation on additional drive

Say that you want to get rid of data written by another user on an hard drive
(e.g. windows installation on F:\).
Open the command line with administration priviledges, then:

    takeown /F F:\Windows /R
    icacls F:\Windows /T /grant /administrators:F
    rd /s F:\Windows

## Modify vbox virtual drive (VDI) dimensions
From host, with virtual machine switched off, show list of virtual disks:

    VBoxManage list hdds

Modify the disk size with:

    VBoxManage modifyhd <uuid/name> --resize <newsize in MB>

Now launch the virtual machine, from guest go to disk manager and expand
the virtual disk with the size just create but not yet allocated.
