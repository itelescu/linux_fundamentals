# Linux notes

- Package managers for Debian, Ubuntu and Linux Mint using **.deb** packages:
    ```
    dpkg - For individual packages file 
    apt-get & apt - will take care of entire dependencies  
    ```

- Package managers for Red Hat, Fedora and CentOS using **.rpm** packages:
    ```
    rpm - For individual packages file 
    dnf & yam - will take care of entire dependencies  
    ```

- Basic Commands:
    Search in package repo for specific package:
    ```
    apt-cash search <package-name>
    ```
    Install and remove package:
    ```
    sudo apt install <package-name>
    sudo apt remove <package-name>
    sudo apt purge <package-name>   To remove config file as well
    ```

- There are 2 major desktop environments **Gnome** and **KDE**, to check your desktop env use:
    ```
    echo $XDG_CURRENT_DESKTOP
    ```
- To get into **TTY** terminal and to exit from the terminal window use:
    ```
    Ctrl + Alt + F1
    Ctrl + Alt + F7
    ```

 ## Shell Types and basic commands

- Default prompt structure looks like this:
    ```
    username@hostname current_directory shell_type

    iontelescu@iontelescu-ThinkPad-T570:~/Side_projects$
    ```
    **username** - name of the user that runs the shell
    **hostname** - name of the host on which shell is running
    **current_directory** - the directory where is currently in, and **~** means current user home directory
    **shell_type** - **$** regular user runs the shell and **#** superuser runs the shell

- Command line structure looks like this:
    ```
    command [option(s)/parameter(s)...] [argument(s)...]
    ```
    Example:
    ```
    ls -l /home
    ```
- There are 2 type of command: 
    INTERNAL - which are build in with shell and are around 30
    EXTERNAL - resides in individual binary files, while calling them shell uses PATH to those files 
    The following command will show what type of command is:
        ```
        $ type echo
        ```
        < echo is shell built in command >

 - Command that will display info about currently logged in user and their activity is:
    ```
    $ w
    ```
    One of the simplest command in linux which shows:
    ![alt text](https://phoenixnap.com/kb/wp-content/uploads/2021/08/w-command-linux-01-output-breakdown.png)


- Quoting:
    - Double quote " "
    - Single quote ' ' 
    - Escaping character \


## Variables

- There are 2 types of variables:
    - Local variable - which are used only in current shell process only
    - Environment variable - used in a current shell and in sub process spawned from shell sessions(other shell opened).Ex : PATH, USER, DATA

To check if variable is local create another shell and call it, if is not displayed this means that this variable is local.

If you close the shell all variables will be lost.

- Creating, calling and unset a variable process is simple:
    ```
    var=key     -setting up variable
    echo $var   -calling variable value
    unset var   -variable still exists but its content is gone
    ```
- Global variable or environment variables can be set using export command:
    ```
    export var=key       - setting up global variable
    echo $var            - call global variable
    bash -c "echo $var"  - call global variable in another shell to make sure is still available in different subprocess
    TZ=EST date          - call global variable in combination with a command
    ```
- PATH variable is like to set ENVIRONMENT VARIABLE on windows, the idea is that this paths variables are list of directories where shell is looking for to invoke commands, if the path for a specific command is missing or deleted unintentionally then shell will not know the command and where to find it.

- To add, remove and call the path use following commands:
    ```
    echo $PATH                          -call PATH                                 
    PATH=$PATH:/home/user/local/bin     -add new path to PATH
    which nano                          -where shell is looking for nano
    PATH=/usr/local/sbin:/usr/local/bin -removing some path by adding not full list of paths to PATH 
    ```

- To substitute a command as a variable value use:
    ```
    nr_files=$(pwd)       -modern option
    nr_files='pwd'        -old option
    ```
- To append a value of a variable to another with a delimiter:
    ```
    ME=$USER              -set a variable     
    ME+=:$HOME            -one method of appending
    ME=$ME:$HOME          -second method of appending
    ```

## Guidance and Help in Linux 

- There are 3 major commands for getting help and additional information about linux commands.
    ```
    --help          - will display general information 
    man mkdir       - manual page information in details for each command or package
    info mkdir      - information page in details about commands or packages
    ```

- Most documentation is stored in **/usr/share/doc/**

- To find the location of the file, there are 2 commands which basically do the same thing with a small difference:
    ```
    locate Desktop              - looking in database for the necessary file or directory
    sudo updatedb               - update db
    locate *Desktop*
    find -name Desktop          - looking in current directory and its subdirectory
    find . -name Desktop        - looking in current directory and its subdirectory
    find ~ -name Desktop        - looking in user home directory
    ```
## Files and directories intro

- Absolute and relative paths can be recognized be /:
    ```
    /home/iontelescu/Side_projects      - absolute path starts with /
    Side_projects/Concepts              - relative path
    .                                   - relative path for current location
    ..                                  - relative path indicates parent directory
    ```
 A **file** is a collection of data with a name and set of attributes. Directories are files that organize other files.

 - Creating directories is easy:
    ```
    mkdir shell_test                - command to create directory shell_test
    mkdir -p new_folder/new_file    - create new folder in another folder using -p or --parent argument
    ```
- Writing to a file:
    ```
    echo hello world > file1        - writing to a file, it will overwrite the content 
    cat file1                       - it will display content from the file 
    ```
- Renaming files and directories:
    ```
    touch file1 file2           - create 2 files
    echo hello > file10         - create one file by writing 'hello' in it
    mv -i file2 file10          - replace content of one file with another and using -1 prompt to be asked if I want to overwrite the content 
    ```
    ```
    mkdir shell_test                    - create a directory
    mv file1 file2 file3 shell_test     - move 3 files into one directory, the last argument is always a directory
    ```