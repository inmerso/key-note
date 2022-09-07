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

## Put latest g++
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt update
    sudo apt install g++-11

## Difference between binary files
    cmp -l file1.bin file2.bin

## Disk usage from current directory
    du -sh *

## Disk usage per partition
    df -h
    
## Print end of file and follow file updates
    tail -f temp.log

## List the top 10 largest file in foldername
    du -a /foldername/ | sort -n -r | head -n 10

# Windows

## ```history``` under windows
    doskey /history

## Delete directories (including subdirectories and files)

Use CMD as *Administrator*.
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

## Locate files

Typical syntax for find commands look like this:

    find command options startingpath expression

For instance, to locate files based on name or extensions:

    find /home/luca/ -name "*.bak"

Basic examples can be:

    find . -name filename.vhdl

    find /home -name *.p4

    find . -type f -empty

Find all .db files changed by *luca* 6 days ago:
    
    find /home -user luca -mtime 6 -iname ".db"

### Optimization options:
- -O1 (default) based on file name first
- -O2 file name first, then file type
- -O3 automatically reorder the search based on efficient use of resources and
likelihood of success

### Other Options:
- -maxdepth N: search in subdirectoriess to a level N
- -iname: case insensitive
- -not: match negation
- type:
    - -type f: search for files
    - -type d: search for directories

### Apply command to matching content

Example to locate and then process, for instance, alter permissions of the find
results:

    find . -name "filename.ext" -exec chmod o+r '{}' \;

The same but ask:

    find . name "filename.ext" -exec -ok chmod o+r '{}' \;

Find then delete:

    find . -type f -name "*.bak" -exec rm -f {} \;

or

    find . -type f -name "*.bak" -delete

Search every file then grep the *searchstring* for every matching file, then
prints them on shell. Curly brakets are the placeholder for *find* results, they
go inside single-quotes so that grep isn't fiven a misshapen file name.
Then exec command is ended with a semicolon, which need an escape so that it
does'nt end up beinng interpreted by the shell.

    find . -type f -exec grep "searchstring" '{}' \; -print


# Mac OS

## Install homebrew
```
$ ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"
```

### Uninstall
```
cd `brew --prefix`
rm -rf Cellar
brew prune
rm `git ls-files`
rm -r Library/Homebrew Library/Aliases Library/Formula Library/Contributions
rm -rf .git
rm -rf ~/Library/Caches/Homebrew
```

## Work with CV
```
$ brew doctor
$ brew install ffmpeg
$ brew install opencv
```

# python
Check the system/OS name to determine where the code is running
```py
from sys import platform

platform.system()

if platform == "linux" or platform == "linux2":
    print("I'm Linux")
elif platform == "darwin":
    # OS X
    pass
elif platform == "win32":
    print("I'm Windows")
```

In python 3.10:
```py
from sys import platform

match platform:
    case "linux" | "linux2":
        print("I'm Linux")
    case "darwin":
        # OS X
        pass
    case "win32":
        print("I'm Windows")
```

### Performance measurement
```py
import time
start = time.perf_counter()
...
end = time.perf_counter()
print(f"Exp time: {end-start} s")
```

# git

## New repository with existing files
1. Create new repo on github
1. Init local
```
git init
git add .
git commit -m "initial commit"
```
1. ``` git remote add origin *url* ```
1. ```git push origin master```

## delete remote branch
    $ git branch -a
    remote/origin/_this_
    $ git push origin --delete _this_

"--delete" can be shortened to "-d".
