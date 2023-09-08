---
layout: post
title: Linux Shell and Bash
description: A Tech Talk on Linux and the Bash shell.
toc: True
comments: True
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 1}, 'csp': {'week': 0, 'categories': ['6.B']}, 'csa': {'week': 0}}
type: hacks
---

## Bash Tutorial
> A brief overview of Bash, on your way to becoming a Linux expert.  When a computer boots up, a kernel (MacOS, Windows, Linux) is started.  This kernel provides a shell that allows user to interact with a most basic set of commands.  Typically, the casual user will not interact with the shell as a Desktop User Interface is started by the computer boot up process.  To activate a shell directly, users will run a "terminal" through the Desktop. VS Code provides ability to activate "terminal" while in the IDE.

## Prerequisites
> Setup bash shell dependency variables for this page.

- Hack: Change variables to match your project.


```python
%%script bash

# Dependency Variables, set to match your project directories

cat <<EOF > /tmp/variables.sh
export project_dir=$HOME/Docuemnts/vscode  # change vscode to different name to test git clone
export project=\$project_dir/student  # change teacher to name of project from git clone
export project_repo="https://github.com/will-w-cheng/student.git"  # change to project of choice
EOF
```


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

# Access the variables
echo "Project dir: $project_dir"
echo "Project: $project"
echo "Repo: $project_repo"
```

    Project dir: /home/will/Docuemnts/vscode
    Project: /home/will/Docuemnts/vscode/student
    Repo: https://github.com/will-w-cheng/student.git


## Setup Project
> Pull code from GitHub to your machine. This script will create a project directory and add "project" from GitHub to the vscode directory.  There is conditional logic to make sure that clone only happen if it does not (!) exist.


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Using conditional statement to create a project directory and project"

cd ~    # start in home directory

# Conditional block to make a project directory
if [ ! -d $project_dir ]
then 
    echo "Directory $project_dir does not exists... makinng directory $project_dir"
    mkdir -p $project_dir
fi
echo "Directory $project_dir exists." 

# Conditional block to git clone a project from project_repo
if [ ! -d $project ]
then
    echo "Directory $project does not exists... cloning $project_repo"
    cd $project_dir
    git clone $project_repo
    cd ~
fi
echo "Directory $project exists." 
```

    Using conditional statement to create a project directory and project
    Directory /home/will/Docuemnts/vscode does not exists... makinng directory /home/will/Docuemnts/vscode
    Directory /home/will/Docuemnts/vscode exists.
    Directory /home/will/Docuemnts/vscode/student does not exists... cloning https://github.com/will-w-cheng/student.git


    Cloning into 'student'...


    Directory /home/will/Docuemnts/vscode/student exists.


### Look at files Github project
> All computers contain files and directories.  The clone brought more files from cloud to your machine.  Review the bash shell script observe the commands that show and interact with files and directories.

- "ls" lists computer files in Unix and Unix-like operating systems
- "cd" offers way to navigate and change working directory
- "pwd" print working directory
- "echo" used to display line of text/string that are passed as an argument


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list top level or root of files with project pulled from github"
ls

```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/will/Docuemnts/vscode/student
    
    list top level or root of files with project pulled from github
    Gemfile
    LICENSE
    Makefile
    README.md
    _config.yml
    _data
    _includes
    _layouts
    _notebooks
    _posts
    activate.sh
    csa.md
    csp.md
    csse.md
    images
    index.md
    indexBlogs.md
    scripts


### Look at file list with hidden and long attributes
> Most linux commands have options to enhance behavior

[ls reference](https://www.rapidtables.com/code/linux/ls.html)


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list all files in long format"
ls -al   # all files -a (hidden) in -l long listing
```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/will/Docuemnts/vscode/student
    
    list all files in long format
    total 100
    drwxr-xr-x 12 will will 4096 Aug 28 23:35 .
    drwxr-xr-x  3 will will 4096 Aug 28 23:35 ..
    drwxr-xr-x  8 will will 4096 Aug 28 23:35 .git
    drwxr-xr-x  3 will will 4096 Aug 28 23:35 .github
    -rw-r--r--  1 will will  104 Aug 28 23:35 .gitignore
    drwxr-xr-x  2 will will 4096 Aug 28 23:35 .vscode
    -rw-r--r--  1 will will  122 Aug 28 23:35 Gemfile
    -rw-r--r--  1 will will 1081 Aug 28 23:35 LICENSE
    -rw-r--r--  1 will will 3008 Aug 28 23:35 Makefile
    -rw-r--r--  1 will will 5798 Aug 28 23:35 README.md
    -rw-r--r--  1 will will  496 Aug 28 23:35 _config.yml
    drwxr-xr-x  2 will will 4096 Aug 28 23:35 _data
    drwxr-xr-x  2 will will 4096 Aug 28 23:35 _includes
    drwxr-xr-x  2 will will 4096 Aug 28 23:35 _layouts
    drwxr-xr-x  3 will will 4096 Aug 28 23:35 _notebooks
    drwxr-xr-x  3 will will 4096 Aug 28 23:35 _posts
    -rwxr-xr-x  1 will will 1291 Aug 28 23:35 activate.sh
    -rw-r--r--  1 will will   92 Aug 28 23:35 csa.md
    -rw-r--r--  1 will will   98 Aug 28 23:35 csp.md
    -rw-r--r--  1 will will  108 Aug 28 23:35 csse.md
    drwxr-xr-x  2 will will 4096 Aug 28 23:35 images
    -rw-r--r--  1 will will 1472 Aug 28 23:35 index.md
    -rw-r--r--  1 will will   53 Aug 28 23:35 indexBlogs.md
    drwxr-xr-x  3 will will 4096 Aug 28 23:35 scripts



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for posts"
export posts=$project/_posts  # _posts inside project
cd $posts  # this should exist per fastpages
pwd  # present working directory
ls -l  # list posts
```

    Look for posts
    /home/will/Docuemnts/vscode/student/_posts
    total 20
    -rw-r--r-- 1 will will 1812 Aug 28 23:35 2023-08-15-Tools_Sprint.md
    -rw-r--r-- 1 will will 4397 Aug 28 23:35 2023-08-16-Tools_Equipment.md
    -rw-r--r-- 1 will will  468 Aug 28 23:35 2023-08-21-GitHub_Pages.md
    -rw-r--r-- 1 will will 3294 Aug 28 23:35 2023-08-21-Java_Caculator.md



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for notebooks"
export notebooks=$project/_notebooks  # _notebooks is inside project
cd $notebooks   # this should exist per fastpages
pwd  # present working directory
ls -l  # list notebooks
```

    Look for notebooks
    /home/will/Docuemnts/vscode/student/_notebooks
    total 80
    -rw-r--r-- 1 will will 37170 Aug 28 23:35 2023-08-16-linux_shell.ipynb
    -rw-r--r-- 1 will will 11446 Aug 28 23:35 2023-08-16-python_hello.ipynb
    -rw-r--r-- 1 will will  5415 Aug 28 23:35 2023-08-17-AP-pseudo-vs-python.ipynb
    -rw-r--r-- 1 will will  8461 Aug 28 23:35 2023-08-21-VSCode-GitHub_Pages.ipynb
    -rw-r--r-- 1 will will  2744 Aug 28 23:35 2023-08-22-Python-IO.ipynb
    -rw-r--r-- 1 will will  1417 Aug 28 23:35 2023-08-28-Plan-for-this-week.ipynb


### Look inside a Markdown File
> "cat" reads data from the file and gives its content as output


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"

cd $project
echo "show the contents of README.md"
echo ""

cat README.md  # show contents of file, in this case markdown
echo ""
echo "end of README.md"

```

    Navigate to project, then navigate to area wwhere files were cloned
    show the contents of README.md
    
    ## Blog site using GitHub Pages and Jekyll
    > This site is intended for Students.   This is to record plans, complete hacks, and do work for your learnings.
    - This can be customized to support computer science as you work through pathway (JavaScript, Python/Flask, Java/Spring)
    - All tangible artifact work is in a _posts or in a _notebooks.  
    - Front matter (aka meta data) in ipynb and md files is used to organize information according to week and column in running web site.
    
    ## GitHub Pages
    All `GitHub Pages` websites are managed on GitHub infrastructure. GitHub uses `Jekyll` to tranform your content into static websites and blogs. Each time we change files in GitHub it initiates a GitHub Action that rebuilds and publishes the site with Jekyll.  
    - GitHub Pages is powered by: [Jekyll](https://jekyllrb.com/).
    - Publised teacher website: [nighthawkcoders.github.io/teacher](https://nighthawkcoders.github.io/teacher/)
    
    ## Preparing a Preview Site 
    In all development, it is recommended to test your code before deployment.  The GitHub Pages development process is optimized by testing your development on your local machine, prior to files on GitHub
    
    Development Cycle. For GitHub pages, the tooling described below will create a development cycle  `make-code-save-preview`.  In the development cycle, it is a requirement to preview work locally, prior to doing a VSCode `commit` to git.
    
    Deployment Cycle.  In the deplopyment cycle, `sync-github-action-review`, it is a requirement to complete the development cycle prior to doing a VSCode `sync`.  The sync triggers github repository update.  The action starts the jekyll build to publish the website.  Any step can have errors and will require you to do a review.
    
    ### WSL and/or Ubuntu installation requirements
    - The result of these step is Ubuntu tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/ubuntu/)
    - Run scripts in scripts directory of teacher repo: setup_ubuntu.sh and activate.sh.  Or, follow commands below.
    ```bash
    ## WSL/Ubuntu commands
    # sudo apt install, installs packages for Ubuntu
    echo "=== Ugrade Packages ==="
    sudo apt update
    sudo apt upgrade -y
    #
    echo "=== Install Ruby ==="
    sudo apt install -y ruby-full build-essential zlib1g-dev
    # 
    echo "=== Install Python ==="
    sudo apt-get install -y python3 python3-pip python-is-python3
    #    
    echo "=== Install Jupyter Notebook ==="
    sudo apt-get install -y jupyter-notebook
    
    # bash commands, install user requirements.
    echo "=== GitHub pages build tools  ==="
    export GEM_HOME="$HOME/gems"
    export PATH="$HOME/gems/bin:$PATH"
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    echo "=== Gem install starting, thinking... ==="
    gem install jekyll bundler
    head -30 ./teacher/scripts/activate.sh
    echo "=== !!!Start a new Terminal!!! ==="
    ```
    
    ### MacOs installation requirements 
    - Ihe result of these step are MacOS tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/macos/). Run scripts in scripts directory of teacher repo: setup_macos.sh and activate_macos.sh.  Or, follow commands below.
    ```bash
    # MacOS commands
    # brew install, installs packages for MacOS
    echo "=== Ugrade Packages ==="
    brew update
    brew upgrade
    #
    echo "=== Install Ruby ==="
    brew install chruby ruby-install xz
    ruby-install ruby 3.1.3
    #
    echo "=== Install Python ==="
    brew install python
    #    
    echo "=== Install Jupyter Notebook ==="
    brew install jupyter
    
    # bash commands, install user requirements.
    export GEM_HOME="$HOME/gems"
    export PATH="$HOME/gems/bin:$PATH"
    echo '# Install Ruby Gems to ~/gems' >> ~/.zshrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.zshrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.zshrc
    echo "=== Gem install starting, thinking... ==="
    gem install jekyll bundler
    head -30 ./teacher/scripts/activate.sh
    echo "=== !!!Start a new Terminal!!! ==="
    ```
    
    ### Preview
    - The result of these step is server running on: http://0.0.0.0:4100/teacher/.  Regeneration messages will run in terminal on any save.  Press the Enter or Return key in the terminal at any time to enter commands.
    
    - Complete installation
    ```bash
    bundle install
    ```
    - Run Server.  This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server.  Logging of details will appear in terminal.   A `Makefile` has been created in project to support commands and start processes.
    
        - Start preview server in terminal
        ```bash
        cd ~/vscode/teacher  # my project location, adapt as necessary
        make
        ```
    
        - Terminal output of shows server address. Cmd or Ctl click http location to open preview server in browser. Example Server address message... 
        ```
        Server address: http://0.0.0.0:4100/teacher/
        ```
    
        - Save on ipynb or md activiates "regeneration". Refresh browser to see updates. Example terminal message...
        ```
        Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
            _notebooks/2024-01-04-cockpit-setup.ipynb
        ```
    
        - Terminal message are generated from background processes.  Click return or enter to obtain prompt and use terminal as needed for other tasks.  Alway return to root of project `cd ~/vscode/teacher` for all "make" actions. 
            
    
        - Stop preview server, but leave constructed files in project for your review.
        ```bash
        make stop
        ```
    
        - Stop server and "clean" constructed files, best choice when renaming files to eliminate potential duplicates in constructed files.
        ```bash
        make clean
        ```
    
        - Test notebook conversions, best choice to see if IPYNB conversion is acting up.
        ```bash
        make convert
        ```
    
    end of README.md


### Env, Git and GitHub
> Env(ironment) is used to capture things like path to Code or Home directory.  Git and GitHub is NOT Only used to exchange code between individuals, it is often used to exchange code through servers, in our case deployment for Website.   All tools we use have a behind the scenes hav relationship with the system they run on (MacOS, Windows, Linus) or a relationship with servers which they are connected to (ie GitHub).  There is an "env" command in bash.  There are environment files and setting files (.git/config) for Git.  They both use a key/value concept.

- "env" show setting for your shell
- "git clone" sets up a director of files
- "cd $project" allows user to move inside that directory of files
- ".git" is a hidden directory that is used by git to establish relationship between machine and the git server on GitHub.  


```python
%%script bash

# This command has no dependencies

echo "Show the shell environment variables, key on left of equal value on right"
echo ""

env
```

    Show the shell environment variables, key on left of equal value on right
    
    SHELL=/bin/bash
    WSL_DISTRO_NAME=Ubuntu-22.04
    NAME=MSI
    PWD=/mnt/c/Users/taplet/Documents/vscode/student/_notebooks
    LOGNAME=will
    HOME=/home/will
    LANG=C.UTF-8
    WSL_INTEROP=/run/WSL/603_interop
    TERM=xterm-256color
    USER=will
    SHLVL=1
    WSLENV=
    XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Users/taplet/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/taplet/AppData/Local/Packages/PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0/LocalCache/local-packages/Python310/Scripts:/mnt/c/Program Files (x86)/VMware/VMware Player/bin/:/mnt/c/Program Files (x86)/Common Files/Oracle/Java/javapath:/mnt/c/Program Files/Eclipse Adoptium/jdk-11.0.17.8-hotspot/bin:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/NVIDIA Corporation/NVIDIA NvDLISR:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/Calibre2/:/mnt/c/Program Files/Microsoft SQL Server/150/Tools/Binn/:/mnt/c/Program Files/Microsoft SQL Server/Client SDK/ODBC/170/Tools/Binn/:/mnt/c/Program Files/dotnet/:/mnt/c/Users/taplet/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/taplet/AppData/Local/GitHubDesktop/bin:/mnt/c/Users/taplet/AppData/Local/Programs/Git/cmd:/mnt/c/src/flutter_windows_3.10.1-stable/flutter/bin:/mnt/c/Users/taplet/.dotnet/tools:/mnt/c/Program Files (x86)/VMware/VMware Player/bin/:/mnt/c/Program Files (x86)/Common Files/Oracle/Java/javapath:/mnt/c/Program Files/Eclipse Adoptium/jdk-11.0.17.8-hotspot/bin:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/NVIDIA Corporation/NVIDIA NvDLISR:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/Calibre2/:/mnt/c/Program Files/Microsoft SQL Server/150/Tools/Binn/:/mnt/c/Program Files/Microsoft SQL Server/Client SDK/ODBC/170/Tools/Binn/:/mnt/c/Program Files/dotnet/:/mnt/c/Users/taplet/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/taplet/AppData/Local/GitHubDesktop/bin:/mnt/c/Users/taplet/AppData/Local/Programs/Git/cmd:/mnt/c/src/flutter_windows_3.10.1-stable/flutter/bin:/mnt/c/Users/taplet/.dotnet/tools:/snap/bin
    HOSTTYPE=x86_64
    _=/usr/bin/env



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

cd $project

echo ""
echo "show the secrets of .git"
cd .git
ls -l

echo ""
echo "look at config file"
cat config
```

    
    show the secrets of .git
    total 48
    -rw-r--r-- 1 will will   21 Aug 28 23:35 HEAD
    drwxr-xr-x 2 will will 4096 Aug 28 23:35 branches
    -rw-r--r-- 1 will will  264 Aug 28 23:35 config
    -rw-r--r-- 1 will will   73 Aug 28 23:35 description
    drwxr-xr-x 2 will will 4096 Aug 28 23:35 hooks
    -rw-r--r-- 1 will will 5921 Aug 28 23:35 index
    drwxr-xr-x 2 will will 4096 Aug 28 23:35 info
    drwxr-xr-x 3 will will 4096 Aug 28 23:35 logs
    drwxr-xr-x 4 will will 4096 Aug 28 23:35 objects
    -rw-r--r-- 1 will will  112 Aug 28 23:35 packed-refs
    drwxr-xr-x 5 will will 4096 Aug 28 23:35 refs
    
    look at config file
    [core]
    	repositoryformatversion = 0
    	filemode = true
    	bare = false
    	logallrefupdates = true
    [remote "origin"]
    	url = https://github.com/will-w-cheng/student.git
    	fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "main"]
    	remote = origin
    	merge = refs/heads/main



```python
%%script bash

# This example has error in VSCode, it run best on Jupyter
cd /tmp

file="sample.md"
if [ -f "$file" ]; then
    rm $file
fi

tee -a $file >/dev/null <<EOF
# Show Generated Markdown
This introductory paragraph and this line and the title above are generated using tee with the standard input (<<) redirection operator.
- This bulleted element is still part of the tee body.
EOF

echo "- This bulleted element and lines below are generated using echo with standard output (>>) redirection operator." >> $file
echo "- The list definition, as is, is using space to seperate lines.  Thus the use of commas and hyphens in output." >> $file
actions=("ls,list-directory" "cd,change-directory" "pwd,present-working-directory" "if-then-fi,test-condition" "env,bash-environment-variables" "cat,view-file-contents" "tee,write-to-output" "echo,display-content-of-string" "echo_text_>\$file,write-content-to-file" "echo_text_>>\$file,append-content-to-file")
for action in ${actions[@]}; do  # for loop is very similar to other language, though [@], semi-colon, do are new
  action=${action//-/ }  # convert dash to space
  action=${action//,/: } # convert comma to colon
  action=${action//_text_/ \"sample text\" } # convert _text_ to sample text, note escape character \ to avoid "" having meaning
  echo "    - ${action//-/ }" >> $file  # echo is redirected to file with >>
done

echo ""
echo "File listing and status"
ls -l $file # list file
wc $file   # show words
mdless $file  # this requires installation, but renders markown from terminal

rm $file  # clean up termporary file
```

    
    File listing and status
    -rw-r--r-- 1 will will 809 Aug 28 23:35 sample.md
     15 132 809 sample.md
    
    [0m[0;1;47;90mShow Generated Markdown [0;2;30;47m========================================================[0m
    
    This introductory paragraph and this line and the title above are generated
    using tee with the standard input (<<) redirection operator.
    [0;1;91m- [0;1;91m[0;97mThis [0;97mbulleted [0;97melement [0;97mis [0;97mstill [0;97mpart [0;97mof [0;97mthe [0;97mtee [0;97mbody.
    [0;1;91m- [0;1;91m[0;97mThis [0;97mbulleted [0;97melement [0;97mand [0;97mlines [0;97mbelow [0;97mare [0;97mgenerated [0;97musing [0;97mecho [0;97mwith [0;97mstandard
    [0;97moutput [0;97m(>>) [0;97mredirection [0;97moperator.
    [0;1;91m- [0;1;91m[0;97mThe [0;97mlist [0;97mdefinition, [0;97mas [0;97mis, [0;97mis [0;97musing [0;97mspace [0;97mto [0;97mseperate [0;97mlines. [0;97mThus [0;97mthe [0;97muse [0;97mof
    [0;97mcommas [0;97mand [0;97mhyphens [0;97min [0;97moutput.
          [0;1;91m- [0;1;91m[0;97mls: [0;97mlist [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mcd: [0;97mchange [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mpwd: [0;97mpresent [0;97mworking [0;97mdirectory
          [0;1;91m- [0;1;91m[0;97mif [0;97mthen [0;97mfi: [0;97mtest [0;97mcondition
          [0;1;91m- [0;1;91m[0;97menv: [0;97mbash [0;97menvironment [0;97mvariables
          [0;1;91m- [0;1;91m[0;97mcat: [0;97mview [0;97mfile [0;97mcontents
          [0;1;91m- [0;1;91m[0;97mtee: [0;97mwrite [0;97mto [0;97moutput
          [0;1;91m- [0;1;91m[0;97mecho: [0;97mdisplay [0;97mcontent [0;97mof [0;97mstring
          [0;1;91m- [0;1;91m[0;97mecho [0;97m"sample [0;97mtext" [0;97m>$file: [0;97mwrite [0;97mcontent [0;97mto [0;97mfile
          [0;1;91m- [0;1;91m[0;97mecho [0;97m"sample [0;97mtext" [0;97m>>$file: [0;97mappend [0;97mcontent [0;97mto [0;97mfile
    
    [0m

## List of command commands I will use frequently (hack #2 on the list)
1. **ls**:
   - Command: `ls`
   - Purpose: Lists files and directories in the current directory.
   - Notes: Commonly used options include `-l` for a long listing format, `-a` to show hidden files, and `-h` for human-readable file sizes.

2. **cd**:
   - Command: `cd [directory]`
   - Purpose: Changes the current working directory.
   - Notes: Use `cd ..` to move to the parent directory and `cd ~` to move to the home directory.

3. **pwd**:
   - Command: `pwd`
   - Purpose: Prints the current working directory.
   - Notes: Useful for finding out where you are in the directory structure.

4. **mkdir**:
   - Command: `mkdir [directory_name]`
   - Purpose: Creates a new directory.
   - Notes: Use the `-p` option to create parent directories if they don't exist.

5. **rm**:
   - Command: `rm [file(s)]`
   - Purpose: Removes (deletes) files or directories.
   - Notes: Be cautious when using this command, as deleted files cannot be easily recovered.

6. **cp**:
   - Command: `cp [source] [destination]`
   - Purpose: Copies files or directories from a source location to a destination.
   - Notes: Use the `-r` option to copy directories recursively.

7. **mv**:
   - Command: `mv [source] [destination]`
   - Purpose: Moves files or directories from a source location to a destination.
   - Notes: Can also be used to rename files and directories.

8. **touch**:
   - Command: `touch [file(s)]`
   - Purpose: Creates empty files or updates the access and modification times of existing files.
   - Notes: Useful for quickly creating new files.

9. **cat**:
   - Command: `cat [file(s)]`
   - Purpose: Displays the content of one or more files.
   - Notes: Can also be used to concatenate and display multiple files.

10. **grep**:
    - Command: `grep [pattern] [file(s)]`
    - Purpose: Searches for a specific pattern in one or more files.
    - Notes: Use the `-i` option for case-insensitive search and `-r` for recursive search in directories.

11. **chmod**:
    - Command: `chmod [permissions] [file(s)]`
    - Purpose: Changes the permissions (read, write, execute) of files or directories.
    - Notes: Permissions can be specified using numerical values or symbolic notation.

12. **chown**:
    - Command: `chown [user]:[group] [file(s)]`
    - Purpose: Changes the ownership of files or directories to a specific user and group.
    - Notes: Useful for managing file ownership and permissions.

13. **sudo**:
    - Command: `sudo [command]`
    - Purpose: Executes a command with superuser (administrator) privileges.
    - Notes: Be cautious when using `sudo` as it grants significant system access.



```python
%%script bash
# Show the active Ruby version, MacOS is 3.1.4
ruby -v

# Show active Python version, it needs to be 3.9 or better
python --version

# Setup Python libraries for Notebook conversion
pip install nbconvert  # library for notebook conversion
pip install nbformat  # notebook file utility
pip install pyyaml  # notebook frontmatter

# Show Jupyter packages, nbconvert needs to be in the list
jupyter --version
# Show Kernels, python3 needs to be in list
#jupyter kernelspec list # does not work on Cloud Ubuntu so I will not be showing it

```

    ruby 3.0.2p107 (2021-07-07 revision 0db68f0233) [x86_64-linux-gnu]
    Python 3.10.12
    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: nbconvert in /usr/lib/python3/dist-packages (6.4.0)
    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: nbformat in /usr/lib/python3/dist-packages (5.1.3)
    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (5.4.1)
    Selected Jupyter core packages...
    IPython          : 7.31.1
    ipykernel        : 6.7.0
    ipywidgets       : 6.0.0
    jupyter_client   : 7.1.2
    jupyter_core     : 4.9.1
    jupyter_server   : not installed
    jupyterlab       : not installed
    nbclient         : 0.5.6
    nbconvert        : 6.4.0
    nbformat         : 5.1.3
    notebook         : 6.4.8
    qtconsole        : not installed
    traitlets        : 5.1.1



```python
import os
import subprocess

def check_anaconda_installed():
    return "anaconda" in os.environ.get("PATH", "").lower()

def check_wsl_installed():
    try:
        subprocess.run(["wsl", "--list"], stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True, check=True)
        return True
    except subprocess.CalledProcessError:
        return False

anaconda_installed = check_anaconda_installed()
wsl_installed = check_wsl_installed()

print("Anaconda Installed:", anaconda_installed)
print("WSL Installed:", wsl_installed)

```

    Anaconda Installed: False
    WSL Installed: True



```bash
%%bash

# Import variables for vscode project to utilize
source /tmp/variables.sh

# Change directory to the correct student repo
cd "$project"

# Configure git
git config --global user.email "will-w-cheng@gmail.com"
git config --global user.name "will-w-cheng"

# Add, commit, and push changes
git add .
git commit -m "New changes added!!!!!!, change this message!"
git push # will lag out the jupyter notebook kernel but yeah

echo "Git commands completed."

```

    On branch main
    Your branch is up to date with 'origin/main'.
    
    nothing to commit, working tree clean


## Hack Preparation.
> Review Tool Setup Procedures and think about some thing you could verify through a Shell notebook.
- Come up with your own student view of this procedure to show your tools are installed.
- Name and create notes on some Linux commands you will use frequently.
- Is there anything we use to verify tools we install? Review versions checks.
- Is there anything we could verify with Anaconda?  or WSL?  
- How would you update a repository?  Could you do that in script above?

