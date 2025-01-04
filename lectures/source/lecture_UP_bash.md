---
marp: true
paginate: true

background: ./resources/global/background.jpg
# apply unocss classes to the current slide
class: text-left

drawings:
  persist: false

transition: fade
---

# **Bash** and **Git**

# LHCb **Starterkit** 2024 

## Lecturers:  

### Dr. Uzziel Perez and Dr. Mindaugas Sarpis

---
layout: image-right
image: ./resources/bash/monochrome_light.png
backgroundSize: contain
---

# What is Bash? 

- ### Bash = **Bourne Again shell**

- ### **TL;DR:** Bash is a shell program designed to listen to my commands and do what I tell it to. - [The Bash Academy](https://guide.bash.academy/)

- ### Other Shell Programs: _zsh_, _csh_, _ksh_... 
- ### On macOS/Linux open terminal and you have a bash shell. 
- ### On Windows install **Windows Subsystem for Linux** (WSL)

```bash
wsl --install
``` 

---
layout: image-right
image: ./resources/bash/AFSStorage.png
backgroundSize: contain
---

# What is Lxplus?

- ### _*lxplus*_ is CERN's interactive linux service for all users 
- It is provided by the IT department and you need to request the activation of "AFS Workspaces" and of 
lxplus and linux for your account through the [CERN Resource Portal](https://resources.web.cern.:x
ch/resources/Manage/ListServices.aspx)
- Also extremely helpful to get some `eos/CERNBox` storage as well 
- List Services &rarr; AFS Workspaces &rarr; Settings 



---
layout: two-cols
---

#  Checking the manual 

Open the terminal and let's get right on to it! 

First command to learn: 

```bash
man bash
```

This shows the documentation on Bash including all the options that can be used with this command.
## SSH: Connecting to a remote computer 

```bash
man ssh
```

**SSH** or Secure Shell is a protocol used to securely connect to a remote computer or server over an unsecured network.  


::right:: 

```bash {*}{maxHeight:'450px', maxWidth:'50px'}
NAME
       bash - GNU Bourne-Again SHell

SYNOPSIS
       bash [options] [command_string | file]

COPYRIGHT
       Bash is Copyright (C) 1989-2020 by the Free Software Foundation, Inc.

DESCRIPTION
       Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file.  Bash also incorporates use‐
       ful features from the Korn and C shells (ksh and csh).

       Bash is intended to be a conformant implementation of the Shell and Utilities portion of the IEEE POSIX specification (IEEE  Standard  1003.1).   Bash
       can be configured to be POSIX-conformant by default.

OPTIONS
       All  of  the  single-character  shell  options documented in the description of the set builtin command, including -o, can be used as options when the
       shell is invoked.  In addition, bash interprets the following options when it is invoked:

       -c        If the -c option is present, then commands are read from the first non-option argument command_string.  If there  are  arguments  after  the
                 command_string,  the first argument is assigned to $0 and any remaining arguments are assigned to the positional parameters.  The assignment
                 to $0 sets the name of the shell, which is used in warning and error messages.
       -i        If the -i option is present, the shell is interactive.
       -l        Make bash act as if it had been invoked as a login shell (see INVOCATION below).


```

---

---
layout: two-cols
---

#  SSH to LXPLUS


```bash
ssh -XY USERNAME@lxplus.cern.ch
```

You can read from 
```bash 
man ssh 
```

what the flags after ssh are for. 

```

```

- ## Accessing the Grid 

To access the grid, we need to initialize a valid **Grid Proxy Certificate** which is essential for accessing various LHCb and CERN computing resources (data storages, job submission and file transfer). 

```bash
lhcb-proxy-init 
```

This command is a wrapper around the standard `voms-proxy-init`. You should see a similar output as on the right.

::right:: 

```bash {*}{maxHeight:'450px', maxWidth:'50px'}
ciperez:~$ lhcb-proxy-init
Generating proxy...
Enter Certificate password: **********
Added VOMS attribute /lhcb/Role=user
Uploading proxy..
Proxy generated:
subject      : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez/CN=2572271230/CN=3271731157
issuer       : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez/CN=2572271230
identity     : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez
timeleft     : 23:53:59
DIRAC group  : lhcb_user
path         : /tmp/x509up_u81686
username     : ciperez
properties   : NormalUser, PrivateLimitedDelegation
VOMS         : True
VOMS fqan    : ['/lhcb/Role=user']

Proxies uploaded:
 DN                                                                                    | Until (GMT)
 /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez | 2025/10/15 12:12

```

---
layout: image-right
image: ./resources/bash/loginlxplus.png
backgroundSize: contain
---

# Quick Checks

To make sure we're all on the same page open your terminal and do the following: 

Now let's log-in to lxplus
```bash
ssh -XY USERNAME.lxplus.cern.ch
lhcb-proxy-init
```

If you've got things set-up before the school, you should see: 

```bash {*}{maxHeight:'450px', maxWidth:'50px'}
Generating proxy...
Enter Certificate password: **********
Added VOMS attribute /lhcb/Role=user
Uploading proxy..
Proxy generated:
subject      : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez/CN=2572271230/CN=3271731157
issuer       : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez/CN=2572271230
identity     : /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez
timeleft     : 23:53:59
DIRAC group  : lhcb_user
path         : /tmp/x509up_u81686
username     : ciperez
properties   : NormalUser, PrivateLimitedDelegation
VOMS         : True
VOMS fqan    : ['/lhcb/Role=user']

Proxies uploaded:
 DN                                                                                    | Until (GMT)
 /DC=ch/DC=cern/OU=Organic Units/OU=Users/CN=ciperez/CN=773459/CN=Cilicia Uzziel Perez | 2025/10/15 12:12
```

---
layout: two-cols
---

# Bash Commands 

- ### Show who runs the script

```bash
whoami 
```
vs
```bash
$USER.
```

- ### Enhance your Terminal Productivity! 
See keyboard shortcuts on the right and for a more exhaustive list [Terminal](https://keycombiner.com/collections/terminal/).

<!-- In the next few slides:

- ### File System Navigation
- ### Modifying Files & Directories
- ### Piping
- ### Regular Expressions -->


::right:: 

```bash {*}{maxHeight:'450px', maxWidth:'50px'}
- ### Keyboard Commands and Navigation

- `Up Arrow`: Will show your last command
- `Down Arrow`: Will show your next command
- `Tab`: Will auto-complete your command
- `Ctrl + L` or `clear`: Will clear the screen
- `Ctrl + C`: Will cancel a command
- `Ctrl + R`: Will search for a command
- `Ctrl + D`: Will exit the terminal

- ### Cursor 
- `Ctrl + A`: Go to the beginning of the command line 
- `Ctrl + E`: Go to the end of the command line 
- `Ctrl + B`: Move back one character 
- `Ctrl + F`: Move forward one character 
- `alt + right`: Move cursor forward one word 
- `alt + left`: Move cursor back one word

- ### History 
- `history` : to print out entire history
- `Ctrl + r`: search command history

```



---
layout: full
---

#  File System navigation 

Commands to navigate the file system. If you are using `lxplus`, you are most-likely 
using the **AFS** or the _Andrew File System_ which is a distributed file system where multiple computers are allowed to share files and data efficiently.

```bash {*}{maxHeight:'450px', maxWidth:'70px'}

| Command                             | Description                                                                       |
| ----------------------------------- | --------------------------------------------------------------------------------- |
| pwd                                 | Lists the path to the working directory                                           |
| ls                                  | List directory contents                                                           |
| ls -a                               | List contents including hidden files (Files that begin with a dot)                |
| ls -l                               | List contents with more info including permissions (long listing)                 |
| ls -r                               | List contents reverse order                                                       |
| cd                                  | Change directory to home                                                          |
| cd [dirname]                        | Change directory to specific directory                                            |
| cd ~                                | Change to home directory                                                          |
| cd ..                               | Change to parent directory                                                        |
| cd -                                | Change to previous directory (which could be different than the parent of course) |
| find [dirtosearch] -name [filename] | Find location of a program                                                        |

```
One can also group flags together like `ls -la`. [Credits to _bradtraversy_ for this slide.](https://gist.github.com/bradtraversy/cc180de0edee05075a6139e42d5f28ce) 

<!-- 
::right:: -->

<!-- ![](./resources/git/git-staging-area.svg) -->

---
layout: center
---

#  Modifying files and directories 

Below are a list of commands to modify files and directories.

```bash {*}{maxHeight:'450px', maxWidth:'70px'}

| Command                     | Description                                         | Examples                   |
| --------------------------- | --------------------------------------------------- | -------------------------- |
| mkdir [dirname]             | Make directory                                      | mkdir starterkit24         |
| touch [filename]            | Create file                                         | touch scratch.py           |
| rm [filename]               | Remove file                                         | rm scratch.py              |
| rm -i [filename]            | Remove directory, but ask before                    | rm -i scratch.py           |
| rm -r [dirname]             | Remove directory                                    | rm -r startkerkit24        |
| rm -rf [dirname]            | Remove directory with contents                      | .....                      |
| rm ./\*                     | Remove everything in the current folder             | 
| cp [filename] [dirname]     | Copy file                                           | 
| mv [filename] [dirname]     | Move file                                           |
| mv [dirname] [dirname]      | Move directory                                      |
| mv [filename] [filename]    | Rename file or folder                               |
| mv [filename] [filename] -v | Rename Verbose - print source/destination directory |
```
We can also do multiple commands at once with the `&&` operator. [Credits to _bradtraversy_ for this slide.](https://gist.github.com/bradtraversy/cc180de0edee05075a6139e42d5f28ce).

---
layout: two-cols
---

# Display and Redirection 


<!-- - ### Redirecting 
``` bash
echo "First line" > file.txt       # Creates/overwrites file
echo "Second line" >> file.txt     # Appends to file
``` -->


- ###  To display messages 
  
  ```bash
  echo "Hello, My name's Forrest."
  ```

- ### To create a file with Echo
  
  ```bash
  echo "Hello, My name's Forrest." > helloworld.txt
  ```

- ### To append to a file
    
    ```bash
    echo "Forrest Gump." >> helloworld.txt
    ```
- ### To display the content of the file
  ``` bash 
  cat helloworld
  ```
In general the right angle bracket tells the system to output results into a target. 


::right::

```bash
echo "  /\___/\ "
echo " (  o o  )"
echo " (  =^=  )"
echo "  --m-m-- "
```

To save the cat into a file:

```bash
echo -e " /\\___/\\\n(  o o  )\n(  =^=  )\n (--m-m--)" > cat.txt
```

Here's a dog:
```
echo -e "  ___________________
< Hello, nice to meet you! >
  -------------------
     \\   ^__^
      \\  (oo)\\_______
         (__)\\       )\\/\\
             ||----w |
             ||     ||"
```

---
layout: two-cols
---

# Piping and Cat 

Like the Force, Piping flows through the terminal, connecting commands together. It's a pathway to many abilities some consider to be... unnatural. Let's use R2-D2 to help us organize some Imperial documents.

First, let's create 10 Death Star plans:
  ```bash
  touch deathstar-plans-{001..010}.txt

  .---.
      /    |\          
      |    | \         .-'''-.
      |    |  \       /   <0> \ 
      |    |   \     /  .---.  \    BEEPS: "Now piping data..."
      |    |    \   /  /     \  \
                 \ /  /       \  \
                  '  /         \  \
                  \  |         |  |
                   | |         |  |
                   |_|         |__|
  ```

  

::right::
Now, let's use R2-D2 to pipe these secret plans into a secure Rebel database file named 
```bash 
find . -name "deathstar-plans-*" > rebel_intel.txt
cat rebel_intel.txt

# Search plans for weakness references
cat rebel_intel.txt | grep "exhaust-port"

# Count total number of stolen plans
ls deathstar-plans* | wc -l

# Sort plans by security level and send to R2
cat rebel_intel.txt | sort | R2D2-encrypt
```
<!-- # Command Reference Table -->
```

| Command | Description                                    | 
| --------| -----------------------------------------------|
| cat     | Displays file content, concatenate files       |
| grep    | Search for patterns, filter matching lines     |
| wc      | Count words (w)/lines (l)/chars (c)            | 
| sort    | Sort lines of text (-r, reverse, -n, numeric)  |
```

---
layout: center
---

#  More commands 

Below are a list of commands to modify files and directories.

```bash {*}{maxHeight:'450px', maxWidth:'70px'}

| Command                            | Description                           | Examples                              |
| -----------------------------------| --------------------------------------| ------------------------------------- |
| grep [pattern][file]               | Looks for a pattern in file           | grep "exhaust-port" rebel_intel.txt   |
| find [directory] -n[name]          | Finds a file in directory             | find . -n rebel_intel.txt             |
| sed "s/[find]/[replace]/g" [file]  | Find and replace a pattern in a text  | sed "s/Luke/Leia/g" rebel_intel.txt   |
| ln -s [filename] [symlinkname]     | Create a symlink                      | ln -s [rebel_intel.txt][rebel.txt]    |
| history                            |

```
 * `grep` is short for _global regular expression print_. It is a useful command to search for matching patterns in a file.
 * `sed` stands for _stream editor_ and it can be used to edit text files. It is commonly used to replace occurences of words in a file.  
 * Creating a symlink is neat way to create shortcut to the original file without having to copy the file.
 * To run the 100th command in history, one can do `!100`

---
layout: center
---

# Jedi Terminal Arts 

- ## Loops Clone Army

```bash
echo "Creating Clone Army..." > clone_trooper.txt
for i in {1..100}; do echo "CT-$i reporting for duty" >> clone_trooper.txt; done
```


- ## The Force Redirect (Advanced Output)
```bash
echo "These aren't the droids you're looking for" >> kenobi_mind_tricks.txt
```


- ## Lightsaber Grep (Search)
```bash
grep -r "rebellion" ./* | echo "⚔️  Lightsaber found these matches:"
```

---
layout: default
---

# Jedi Mind Tricks

```bash
ps aux | grep "imperial-spy"    # Find Imperial processes
kill -9 $imperial_pid           # Use Force choke

# Vader's File Permissions
chmod 777 death_star_plans.txt  # Grant all access
chown luke skywalker.txt        # Transfer ownership

# Millennium Falcon Data Transfer
# Open a new terminal and secure copy death_star_plans.txt to your Desktop

cd ~/Desktop
scp . jediusername@lxplus.cern.ch<afspath/to/>/death_star_plans.txt 
rsync -avz rebel_base/ backup_base/    # Always have a backup plan
```
```bash
.=.
      '==c|
      [)-+|
      /'/\|
     /  /\|
    /  /  |
   /  /  /|
  /  /  / |
 /__/__/  |
<._._._,_/>  BB-8: "Beep boop - executing commands!"

```


---
layout: default
---

# Head and Tail 



```bash
  head [filename]
```

You can also specify the number of lines to output:

```bash
  head -n 5 [filename]
```

The `tail` command is used to output the last part of files. By default, it outputs the last 10 lines of each file. You can also specify the number of lines to output.

```bash
  tail [filename]
```

You can also specify the number of lines to output:

```bash
  tail -n 5 [filename]
```

Let's make 100 Clone Troopers and print out the first 3 lines and the last 5 lines in the list.
```bash
echo "Creating Clone Army..." > clone_trooper.txt
for i in {1..100}; do echo "CT-$i reporting for duty" >> clone_trooper.txt; done
head -n 3 clone_trooper.txt  && tail -n 5 clone_trooper.txt
```





---
layout: default
backgroundSize: contain
---
# Other Comands 



```bash 
| Command     | Description                                                     |           /      \__
| ----------- | --------------------------------------------------------------- |          /   []     |
| ps          | a.k.a. process status displays all processes                    |          |          |
| ps aux      | display all processes in the system, of aux flags.              |          |    ______|
| chmod       | change file modes                                               |          |    ______|
| chmod u+x   | give yourself (owner only) permission to execute a file you own |          /    |____  
| chmod +x    | Adds permission to execute a file = `chmod a+x`                 |         /     ____|
| chown       | change file onwer or group                                      | |\     /     |_
| top         | display sorted information about processes                      | | \   /        /\
| kill <pid>  | terminate or kill a signal process                              | |  \_/        |  []
| kill -9     | non-ignorable kill!                                             | |             |
| lsof +D     | list open files. Useful when prematurely killing a process      |  \           /
| tar         | manipulate tape archives                                        |   \         / 
| zip         | package and compresss archive files                             |    \  ___ |
                                                                                      | |  \|
                                                                                      |/    |
                                                                                      |_    |_
                                                                                      [_]   [_]
```

---
layout: fact
---

Bash scripting is a powerful way to automate tasks on Linux and can be used in endless ways and boosts productivity and having basic knowledge of it is important if you’re planning on becoming an ethical hacker or system administrator or simply want to automate tedious boring tasks and we’ll hopefully explore more in later blogs and build interesting tools with it - **moo**, some guy on [medium](https://medium.com/geekculture/bash-scripting-for-dummies-5d855cbada66)


---
layout: two-cols
---
# Bash Scripting Crash Course

Inspired by the [Missing Shell Scripting Crash Course](https://dev.to/godcrampy/the-missing-shell-scripting-crash-course-37mk)


- ## Variable 
Assigning value to a variable needs `$`, otherwise bash will treat name as a string literal and it will output `Hello name` instead.
```bash 
#!/bin/bash
name ="Luke Skywalker"
echo "Hello, $name"
```

To run,  
```bash
$user chmod
$user ./script.sh
```
::right::

- ## User input

```bash
read -p "What is you name: " name
echo "Hello $name"

read -p "Enter an action: " verb
echo "You are ${verb}ing"
```
- ## Arguments

`$1, $2..` store the arguments passed to the script... 

```bash
echo $0
echo $1
echo $2
echo "${@}" # Access all the arguments [More on this later]
```

So if you do `./script.sh condition1 condition2`, what happens? It just echos the strings passed on to the script.

---
layout: two-cols
---
# Bash Scripting Crash Course

Inspired by the [Missing Shell Scripting Crash Course](https://dev.to/godcrampy/the-missing-shell-scripting-crash-course-37mk)


- ## Logical Comparisons 

* [[]] enables to use operators. 
*  Comparisons: `=, !=, >, <, ≤, ≥`
* Leave some space on both ends of brackets.. :) 

```bash 
if [[ "$name" == "adam driver" ]]
then
   echo "hi adam we missed you"
else
   echo "welcome $name"
fi
```

::right::

- ## Test commands for some complex operations

```bash
[[ -e "$file" ]] # True if file exists
[[ -d "$file" ]] # True if file exists and is a directory
[[ -f "$file" ]] # True if file exists and is a regular file
[[ -z "$str" ]]  # True if string is of length zero
[[ -n "$str" ]]  # True is string is not of length zero

# Compare Strings
[[ "$str1" == "$str2" ]]
[[ "$str1" != "$str2" ]]

# Integer Comparisions
[[ "$int1" -eq "$int2" ]] # $int1 == $int2
[[ "$int1" -ne "$int2" ]] # $int1 != $int2
[[ "$int1" -gt "$int2" ]] # $int1 > $int2
[[ "$int1" -lt "$int2" ]] # $int1 < $int2
[[ "$int1" -ge "$int2" ]] # $int1 >= $int2
[[ "$int1" -le "$int2" ]] # $int1 <= $int2

# And or 
[[ ... ]] && [[ ... ]] # And
[[ ... ]] || [[ ... ]] # Or
```


---
layout: two-cols
---
# Bash Scripting Crash Course

Inspired by the [Missing Shell Scripting Crash Course](https://dev.to/godcrampy/the-missing-shell-scripting-crash-course-37mk)


- ## Arrays and Functions

```bash 
arr=(a b c d)
```

To read: 

```bash
echo "${arr[1]}"     # Single element
echo "${arr[-1]}"    # Last element
echo "${arr[@]:1}"   # Elements from 1
echo "${arr[@]:1:3}" # Elements from 1 to 3
```

To insert: 
```bash 
arr[5]=e                            # direct address and insert/update
arr=(${arr[@]:0:1} new ${arr[@]:1}) # Adding 'new' to array
```

To delete:
```bash
arr=(a b c d)
unset arr[1]
echo << "${arr[1]}" # Outputs nothing
```

::right::

- ## Deleting needs re-indexing

```bash
arr=(a b c d)
unset arr[1]
arr=("${arr[@]}")
echo << "${arr[1]}" # c
```
- ## Functions

```bash
greet() {
  echo "Hello, $1"
}

greet Bash # Hello, Bash
```

---
layout: two-cols
---

# Bash Scripting 

Store this cat into a `txt` file.
```bash
 /\_/\
( o o )
 > ^ <
```

::right::

Can you use your Jedi Tricks to make this cat sleep?
Use the `sed` command and store it into another `txt` file.

```bash 


 /\_/\
( X X )
 > ^ <

```



---
layout: two-cols
---

# Cat Exercise

Store this cat into a `txt` file.
```bash
 /\_/\
( o o )
 > ^ <
```

Open a file `<editor> cat_draw.sh`. When creating a bash script, start with a shebang.

```bash
#!/bin/bash

# File to store the cat
cat_file="cat.txt"

# Draw a cat with eyes open and write to the file
cat_open="
 /\\_/\\
( o o )
 > ^ <
"
echo "$cat_open" > $cat_file
echo "Cat with eyes open has been written to $cat_file."
```

::right::
Run the script. 

```bash
chmod +x cat_draw.sh
./cat_draw.sh
```

Check the contents of the `cat_file` with `cat cat_file`. 

Can you use your Jedi Tricks to make this cat sleep?
Use the `sed` command and store it into another `txt` file.

```bash 
# Use sed to replace open eyes (o) with closed eyes (X)
sed "s/o/X/g" $cat_file > sleeping_cat.txt
echo "Cat with eyes closed has been written to sleeping_cat.txt."
cat sleeping_cat.txt


 /\_/\
( X X )
 > ^ <
```

---
layout: two-cols
---

# Shell Scripts 

Write a new script called `my_script.sh` with your favorite editor.

* _Loops_ and _if statements_ need a ";"

```bash
j = 20 
for i in {0..10};
  do
    echo $i
    (( j+= 1))
  done 

if [-f $HOME/.bashrc ];
  then
    echo Have .bashrc
fi 
```

* Variables 
Assigning value to a variable needs `$`

```bash
a = $((j+2))
echo $a, $j
```

::right::

We can add some safety options  at the top of the script. 
```bash 


#!/usr/bin/env bash

# my_script.sh

# Safety options
# -u :Undefined variables are treated as errors 
# script will stop when encountered
# -e: if any commands in the script fail
# the script immediately fails
# -o: pipefail prevents the script from running in pipes

set -eux -o pipefail 
shopt -s expand_aliases
 
j = 20 
for i in {0..10};
  do
    echo $i
    (( j+= 1))
  done 
....

```

---
layout: two-cols
---

# Shell Scripts 

Write a new script called `my_script.sh` with your favorite editor.

* _Loops_ and _if statements_ need a ";"

```bash
j = 20 
for i in {0..10};
  do
    echo $i
    (( j+= 1))
  done 

if [-f $HOME/.bashrc ];
  then
    echo Have .bashrc
fi 
```

* Variables 
Assigning value to a variable needs `$`

```bash
a = $((j+2))
echo $a, $j
```

::right::

We can add some safety options  at the top of the script. 
```bash 


#!/usr/bin/env bash

# my_script.sh

# Safety options
# -u :Undefined variables are treated as errors 
# script will stop when encountered
# -e: if any commands in the script fail
# the script immediately fails
# -o: pipefail prevents the script from running in pipes

set -eux -o pipefail 
shopt -s expand_aliases
 
j = 20 
for i in {0..10};
  do
    echo $i
    (( j+= 1))
  done 
....

```


---
layout: default
---

# Minimal Safe Bash Script Template
A tutorial I wish I had when I was younger is from [Bash Script Template](https://betterdev.blog/minimal-safe-bash-script-template/)

```bash {*}{maxHeight:'450px', maxWidth:'50px'}
#!/usr/bin/env bash

## FAIL FAST
# The set command changes the script execution options
set -Eeuo pipefail
trap cleanup SIGINT SIGTERM ERR EXIT

script_dir=$(cd "$(dirname "${BASH_SOURCE[0]}")" &>/dev/null && pwd -P)

usage() {
  cat << EOF # remove the space between << and EOF, this is due to web plugin issue
Usage: $(basename "${BASH_SOURCE[0]}") [-h] [-v] [-f] -p param_value arg1 [arg2...]

Script description here.

Available options:

-h, --help      Print this help and exit
-v, --verbose   Print script debug info
-f, --flag      Some flag description
-p, --param     Some param description
EOF
  exit
}

cleanup() {
  trap - SIGINT SIGTERM ERR EXIT
  # script cleanup here
}

setup_colors() {
  if [[ -t 2 ]] && [[ -z "${NO_COLOR-}" ]] && [[ "${TERM-}" != "dumb" ]]; then
    NOFORMAT='\033[0m' RED='\033[0;31m' GREEN='\033[0;32m' ORANGE='\033[0;33m' BLUE='\033[0;34m' PURPLE='\033[0;35m' CYAN='\033[0;36m' YELLOW='\033[1;33m'
  else
    NOFORMAT='' RED='' GREEN='' ORANGE='' BLUE='' PURPLE='' CYAN='' YELLOW=''
  fi
}

msg() {
  echo >&2 -e "${1-}"
}

die() {
  local msg=$1
  local code=${2-1} # default exit status 1
  msg "$msg"
  exit "$code"
}

parse_params() {
  # default values of variables set from params
  flag=0
  param=''

  while :; do
    case "${1-}" in
    -h | --help) usage ;;
    -v | --verbose) set -x ;;
    --no-color) NO_COLOR=1 ;;
    -f | --flag) flag=1 ;; # example flag
    -p | --param) # example named parameter
      param="${2-}"
      shift
      ;;
    -?*) die "Unknown option: $1" ;;
    *) break ;;
    esac
    shift
  done

  args=("$@")

  # check required params and arguments
  [[ -z "${param-}" ]] && die "Missing required parameter: param"
  [[ ${#args[@]} -eq 0 ]] && die "Missing script arguments"

  return 0
}

parse_params "$@"
setup_colors

# script logic here

msg "${RED}Read parameters:${NOFORMAT}"
msg "- flag: ${flag}"
msg "- param: ${param}"
msg "- arguments: ${args[*]-}"

```

---
layout: default
---

# Minimal Safe Bash Script Template Walkthrough

* FAIL FAST

```bash
#!/usr/bin/env bash
cp important_file ./backups/
rm important_file
```
Suppose the backups directory does not exist. If there is no safety option `set -Eeuo pipefail`, bash jumps into the next command and deletes the important file before you can react.

* Get the Location
```bash
script_dir=$(cd "$(dirname "${BASH_SOURCE[0]}")" &>/dev/null && pwd -P)
```

Often we find the scripts we need to run in some other directory e.g. `/some/long/path/to/script.sh`. 
This can be fixed by going to the directory before execution with `cd /some/long/path/to/ && ./script.sh`


---
layout: default
---

# Minimal Safe Bash Script Template Walkthrough

* DISPLAY HELPFUL HELP and print nice messages - This is minimal documentation and also to display help for someone to know the options on how to use the script.

```bash
usage() {
  cat << EOF # remove the space between << and EOF, this is due to web plugin issue
Usage: $(basename "${BASH_SOURCE[0]}") [-h] [-v] [-f] -p param_value arg1 [arg2...]
Script description here.
...
EOF
  exit
}
```
```bash {*}{maxHeight:'450px', maxWidth:'50px'}
setup_colors() {
  if [[ -t 2 ]] && [[ -z "${NO_COLOR-}" ]] && [[ "${TERM-}" != "dumb" ]]; then
    NOFORMAT='\033[0m' RED='\033[0;31m' GREEN='\033[0;32m' ORANGE='\033[0;33m' BLUE='\033[0;34m' PURPLE='\033[0;35m' CYAN='\033[0;36m' YELLOW='\033[1;33m'
  else
    NOFORMAT='' RED='' GREEN='' ORANGE='' BLUE='' PURPLE='' CYAN='' YELLOW=''
  fi
}

msg() {
  echo >&2 -e "${1-}"
}
```


---
layout: default
---

# Environment scripts 

One can string together various pieces of their analysis... 

```bash
export analysis_dir=$HOME/work/analysis
alias mainscript="python3 main.py"
lhcb-proxy-init
source setupLCG.sh
function run_analysis(){
  python3 do_Fit.py
  python3 calc_eff.py
  python3 main_analysis.py
  python3 plot_results.py
}
```

---
layout: two-cols
---


# Bash Profile and persistency settings

The `~/.bash_profile` is used for defining user settings for a login shell.

```bash
# .bash_profile
# Load .bashrc if it exists
test -f ~/.bashrc && source ~/.bashrc

# Alternatively 
# Get Aliases and functions 
if [-f ~/.bashrc]; then
  . ~/.bashrc
fi

# User specific environment and startup programs 
PATH=$PATH:$HOME/bin
export PATH
echo "$(date + [%F_%H:%M]) at $(hostname)" >> .lxnodes # useful for tmux session
export PATH=$HOME/.cargo/bin:$PATH"

# Enable text color and formatting
export PS1="\[\033[36m\]\u:\[\033[33m\]\w\[\033[m\]\$ "
export CLICOLOR=true
export LSCOLORS=ExGxBxDxCxEgEdxbxgxcxd
```

::right::

The `~/.bashrc` file provides a place where you can set up variables, functions and aliases and helps reduce redundant effort. 

```bash
 # .bashrc

# This is GOLD for finding out what is taking so much space on your drives!
alias diskspace="du -S | sort -n -r |more"

# This is where you put your hand rolled scripts (remember to chmod them)
PATH="$HOME/bin:$PATH"

alias ll ='ls -l -h'
alias la='ls -a -l -h'

function mcd (){
  mkdir $1; cd $1
}

alias eosuser='cd /eos/user/c/ciperez'
alias afsdir='cd /afs/cern.ch/work/c/ciperez
```

Ref: [stackexchange](https://serverfault.com/questions/3743/what-useful-things-can-one-add-to-ones-bashrc)


---
layout: default
---

# Miscellaneous 

- ## TMUX, Screen
Lets you split session into windows and also lets you log out and having the session running. 
For big workloads, better to use HTCondor. Helps with monitoring CPU/memory usage too.

See a [Quick and Easy Guide to TMUX](https://hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/) and [How to Use Linux Screen](https://linuxize.com/post/how-to-use-linux-screen/).

- ## LCG Stacks and Apptainer 

If you want an environment where everything works harmoniously, you might want to create a conda environment, or a python environment. 

It is however better to rely on the already installed software to work with the platform you currently have. 

```bash
env | grep -i platform
source /cvmfs/sft.cern.ch/lcg/views/setupViews.sh <LCG_number> <platform>
```

For ML related stuff, one can also get gpu-supported programs such as `tensorflow` with `LCG_106cuda for lxplus-gpu`.
To check the latest LCG releases [click here](https://lcginfo.cern.ch/).

---
layout: fact
---

THE END!  
This is just a simulation.
