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
- Renaming and moving files and directories:
    ```
    touch file1 file2           - create 2 files
    echo hello > file10         - create one file by writing 'hello' in it
    mv -i file2 file10          - replace content of one file with another and using -i prompt to be asked if I want to overwrite the content 
    ```
    ```
    mkdir shell_test                    - create a directory
    mv file1 file2 file3 shell_test     - move 3 files into one directory, the last argument is always a directory
    ```
- Copying files and directories:
    ```
    cp test_folder/file1 prod_folder/file1  - copy file from one dir to another
    cp -r folder1 folder2                   - copy recursively folder and its content in another folder, and if the second folder doesn't exist it will create one
    ```
- Globing pattern matching:
    
    *Matches any number of any character, including no characters
    ? Matches any one character
    [ ]Matches a class of characters

    ```
    $ ls
    file1 file2 file99 games10 games1001 games10001
    $ ls file*
    file1 file12 file99
    $ ls file1*
    file12
    $ ls games100*
    games1001  
    $ ls file?
    file1 file2
    $ ls file[1-2]
    file1 file2
    ```
    [:alnum:]
    Letters and numbers.
    [:alpha:]
    Upper or lowercase letters.
    [:blank:]
    Spaces and tabs.
    [:cntrl:]
    Control characters, e.g. backspace, bell, NAK, escape.
    [:digit:]
    Numerals (0123456789).
    [:graph:]
    Graphic characters (all characters except ctrl and the space character)
    [:lower:]
    Lowercase letters (a-z).
    [:print:]
    Printable characters (alnum, punct, and the space character).
    [:punct:]
    Punctuation characters, i.e. !, &, ".
    [:space:]
    Whitespace characters, e.g. tabs, spaces, newlines.

- Additional:
    ```
    rm -v file1 file2                   - verbose mode
    rmdir -p Side_projects/shell_test   - remove recursively using -p param
    mv -n file1 file2                   - file1 will prevent overwriting content of file1 to file2
    ```

## Archiving files

- There are 2 type of compressions: **lossless** and **lossy**, each having on its base different algorithms, in first case your files on the decompression will be restored back in original form, while in the second case decompression will have different output from the original one (ex. Video, audio decompressed files will have different quality than original).
- Archiving bundle together different files into one. The most common tool to compress files in Linux system is **tar** which will not compress the file by default.
- The most used compression tools on Linux are **bzip2**, **gzip**, **xz** all 3 use the same algorithm for compression so you can decompress one by another.
    ```
    bzip2 file_name     - the compression size will be different for each zipped file                
    gzip file_name      - using gzip -1 or gzip -9 will have different level of compression
    xz file_name

    bunzip2 file_name
    gunzip file_name
    unxz file_name
    ```
- Archiving can be performed by using following commands:
    ``` 
    tar -cf <path/archived_folder_name.tar> <required_compress_folder>      - c means new file to be archived and f is the name of the file
    tar -tf <archived_folder_name.tar>                                      - this command will display all the files in the archived file
    tar xf <archived_folder_name.tar>                                       - unarchive file
    tar xvf <archived_folder_name.tar>  <path/file_name>                    - this command will unarchive the specific file only
    ```
- Create compressed archived tar files can be done by following commands:
    j -> bzip2
    J -> xz
    z -> gzip
    ```
    tar -czf compressed_file_name.tar.gz <file_name_to_compress>
    tar -cjf compressed_file_name.tar.bz2 <file_name_to_compress>
    tar -cJf compressed_file_name.tar.xz <file_name_to_compress>

    tar -czf compressed_file_name.tgz <file_name_to_compress>   - tgz extension instead of double extension

    ```

- It is possible to add files to already existing uncompressed tar archives. Use the u option to do this.If you attempt to add to a compressed archive, you will get an error.
    ```
    tar cf file_name.tar <filename1> <filename2>    - archive 2 files 
    tar uf file_name.tar <filename3>                - updated previous archived file with one more file, it works only for uncompressed archived files
    ```