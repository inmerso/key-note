# Linux

## Execute command from history

    history

Execute the command calling by its number in _history_ (e.g. 71):

    $ !71

Execute again last command `$ !!` it is equivalent to `$ !-1`.

Scroll back and forward history with <kbd>⌃ Ctrl</kbd>+<kbd>P</kbd> and 
<kbd>⌃ Ctrl</kbd>+<kbd>N</kbd>.
Reach the end of history with <kbd>⌃ Ctrl</kbd>+<kbd>⇧ Shift</kbd>+<kbd>.</kbd>.

## Get process output

Once you know the PID, with `ps -ax | grep appname`, you can use it:

    tail -f /proc/<pid>/fd/{0:8}


## Find occupied IPs on the network

You'll need _nmap_ for this. To install it:

    sudo snap install nmap

Once installed, you can find all the hosts that respond to ping requests on the
network (IP addresses ranging between 192.168.1.0 to 192.168.1.255) by typing
the following:

    nmap -sn 192.168.1.0/24

## Increase sudo password timeout

If you like to increase timeout of sudo session in terminal, to say 4 hours 
(240 minutes), type:

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

## Print dmesg as it changes

    dmesg -wH

## Minimum ubuntu setup

Everything required for compiling basic software written in C and C++.

    sudo apt install build-essential

Then

    snap install code --classic
    sudo apt install git-all
    sudo apt install picocom
    sudo snap install cmake --classic
    sudo apt install python3-pip

## Notify with sound compilation finished

If you like to have a notification after `make` is done:

    make; spd-say 'done'

## Running a full-screen clock

```bash
    dclock -nobell -nomiltime -tails -noscroll -noblink -nofade -date "%a %b %d, %Y" -noalarm -seconds -bd "black" -bg "black" -fg "red" -led_off "black" &
```


# Windows

## ```history``` under windows

```bat
doskey /history
```

## Delete directories (including subdirectories and files)

Use CMD as *Administrator*.
Navigate into the directory you want to remove (e.g. _foldername_)

```bat
DEL /F/Q/S *
CD ..
RMDIR _foldername_ /Q/S
```

## Get rid of windows installation on additional drive

Say that you want to get rid of data written by another user on an hard drive
(e.g. windows installation on F:\).
Open the command line with administration priviledges, then:

```bat
takeown /F F:\Windows /R
icacls F:\Windows /T /grant /administrators:F
rd /s F:\Windows
```

## Modify vbox virtual drive (VDI) dimensions

From host, with virtual machine switched off, show list of virtual disks:

    VBoxManage list hdds

Modify the disk size with:

    VBoxManage modifyhd <uuid/name> --resize <newsize in MB>

Now launch the virtual machine, from guest go to disk manager and expand
the virtual disk with the size just create but not yet allocated.

## Set permission for virtualbox shared folders

First, configure shared folder, then:

```sh
    sudo adduser $USER vboxsf
```

Then restart.

## Locate files

Typical syntax for find commands look like this:

```sh 
find command options startingpath expression
```

For instance, to locate files based on name or extensions:

```sh
find /home/luca/ -name "*.bak"
```

Basic examples can be:

```sh
find . -name filename.vhdl
find /home -name *.p4
find . -type f -empty
```

Find all .db files changed by *luca* 6 days ago:

```sh    
find /home -user luca -mtime 6 -iname ".db"
```

### Optimization options:

- `-O1` (default) based on file name first
- `-O2` file name first, then file type
- `-O3` automatically reorder the search based on efficient use of resources and
likelihood of success

### Other Options:

- `-maxdepth N`: search in subdirectoriess to a level N
- `-iname`: case insensitive
- `-not`: match negation
- type:
    - `-type f`: search for files
    - `-type d`: search for directories

### Apply command to matching content

Example to locate and then process, for instance, alter permissions of the find
results:

```sh
find . -name "filename.ext" -exec chmod o+r '{}' \;
```

The same but ask:

```sh
find . name "filename.ext" -exec -ok chmod o+r '{}' \;
```

Find then delete:

```sh
find . -type f -name "*.bak" -exec rm -f {} \;
```

or

```sh
find . -type f -name "*.bak" -delete
```

Search every file then grep the *searchstring* for every matching file, then
prints them on shell.
Curly brakets are the placeholder for *find* results, they go inside
single-quotes so that grep isn't fiven a misshapen file name.
Then `exec` command is ended with a semicolon, which need an escape so that it
doesn't end up beinng interpreted by the shell.

```sh
find . -type f -exec grep "searchstring" '{}' \; -print
```

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
# ...code...
end = time.perf_counter()
print(f"Exp time: {end-start} s")
```

# vscode

## Remove empty lines

1. <kbd>⌃ Ctrl</kbd> + <kbd>H</kbd> (find and replace)
1. in find box, type regular expression 
    ```
    ^(\s)*$\n
    ```
1. leave replace box empty
1. <kbd>⌃ Ctrl</kbd> + <kbd>⌥ Alt</kbd> + <kbd>⏎ Enter</kbd> to apply Replace All 

# git

## Where's the origin?

```
git remote -v 
```

## New repository with existing files

1. Create new repo on github
1. Init local
    ```
    git init
    git add .
    git commit -m "initial commit"
    ```
1. ```git remote add origin *url*```
1. ```git push origin master```

## delete remote branch

    $ git branch -a
    remote/origin/_this_
    $ git push origin --delete _this_

"--delete" can be shortened to "-d".

## Export commit history

    $ git log >> history.txt
    
# fun

## Display video in ASCII characters

    mplayer -vo caca <movie_file>
    
## Install file manager

    sudo add-apt-repository ppa:elementary-os/stable
    sudo apt-get update
    sudo apt-get install pantheon-files

