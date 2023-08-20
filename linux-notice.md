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
    help          - will display general information 
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
    tar xf <archived_folder_name.tar>                                       - unarchive file in current working directory
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

## Writing, reading and searching from and to the files

- There are 3 channels to redirect/transmit information from one source to another:
    - **stdin** channel 0 - standard input
    - **stdout** channel 1  - standard output
    - **stderr** channel 2  - redirect the error

    ```
    echo "Hello World" > text_file      - write the input to the file, if it's exist if not it will create one, if it has content it will overwrite
    echo "Hi All" >> text_file          - append input to the file

    find /usr/blackhole 2> file_name    - write the error to the file_name
    find /usr/blackhole 2>> file_name   - append the error to the file_name
    find /usr/blackhole 2> dev/null     - write the error in the file that will erase it instantly 
    
    cat < text_file_name                - redirect the content of the file to the command, only the commands that don't require path argument
    tr -d "lol" < text_file_name        - tr command will translate the file content and modify the characters in a specific way. In this example it will delete occurrence of all "lol" in the file_name
    ```

- To write some configuration or some documentation in a file, use:
    ```
    cat << delimiter                - write line by line until use delimiter and its stops
    cat << delimiter > file_name    - you can write as much information as you want and once you finish write the word instead of delimiter and the file_name will be overwritten with your content
    ```
- Combination of channel1 and channel2 can be done by using & operator:
    ```
    find /etc black_hole_file &> file_name
    find /bin/games &>> file_name
    ```
- Counting words in a file can be done by:
    ```
    wc -w <file_name>       - wc is word count command -w means that it will count words, not bytes or any other type of information
    ```
- Piping is an import part of scripting and command line tools:
    ```
    ls -R | head | wc -l    - this command will count first 10 line of the ls -R result (10 lines because of head command)
    ```
## Searching for a patterns in a file and manipulate text

- Global regular expression patter or grep can display lines of text where the pattern matches and highlight the pattern in red:
    ```
    grep "bash" /etc/passwd                 - display lines where the pattern matches and highlight in red the pattern
    grep -i "bash" /etc/passwd              - display lines with case insensitive 
    grep -E "ba.+" /etc/passwd              - display extended pattern match
    grep "[ab]" /etc/passwd                  
    grep -c -E /etc/passwd                  - display count pattern matches
    grep -E "bash|password" /etc/passwd     - using -E extended regex display either or another match
    grep -r "^ba" /etc/passwd               - starting line with ba will be displayed
    ```
    *Zero or more of the preceding pattern
    +One or more of the preceding pattern
    ?Zero or one of the preceding pattern

    -i  -case insensitive
    -c  -count occurrence of pattern
    -v  -invert the match of the patter
    -r  -recursive search
    -E  -extended regular expression


## Commands into scripts

- Using command in shell command line is one way of executing them, but when you have bigger scripts or commands to execute then it becomes harder to manage them and have them saved, so in this case scripts are coming into help. Like python scripts, we can have bash scripts and files usually have .sh or .bash extensions, also in the beginning of the script, to identify that this is bash script is a good practice to define interpreter using``` #!/bin/bash``` (called shebang).
As you know, in order to execute a file shell is looking into ```$PATH``` variable if the executable is there. There are three solutions to this issue: we can move new_script into one of the PATH directories, we can add our current directory to PATH, or we can change the way we attempt to call the script.
The latter solution is easiest, it simply requires us to specify the current location when calling the
script using dot slash (./)

```
echo 'echo "Hello World!"'> script.sh       - writing script to a file
    
chmod +x script.sh                          - provide permission of execution

./script.sh                                 - execute the script
```

- Variables in bash script are **implicit type** and are considered strings (in order to make them numbers we will need to explicit use **expr** command  or $((...)) expression). 
Also they can be used in this format :
```${variable_name}```
- Don't negligee quotes as those are important in defining variables.
    ```
    #!bin/bash
    username1="Ion Telescu"         - week quoting allow substitution  
    username2='Ion Telescu'         - don't allow substitution in quoting
    username3=Ion Telescu           - will treat it as a separate variable values Ion is first and Telescu is second, which might create unpredictable behavior
    ```
- Arguments allow user to pass them to the executable script:
    ```
    #!bin/bash
    argument=$1
    argument=$2
    echo "first is $argument and second is $argument"

    $./script username password
    first is username and second is password  
    ```
- To return number of arguments use:
    ```
    #!bin/bash
    argument=$1                         - define argument number 1
    argument=$2                         
    echo "number of arguments: $# "     - return number of arguments

    $./script number1 number2
    number of arguments: 2 
    ```
- Simple conditional flow in bash looks different than in other language. If statement has its stop sign which is fi:
    ```
    #!/bin/bash

    usr_number=$1

    if [ $usr_number -gt 10 ];then
        echo "$usr_number is greater than 10"
    elif [ $usr_number -eq 10 ];then
        echo "$usr_number is 10"
    else
        echo "$usr_number is smaller than 10" 
    fi
        echo "script is stopping here"
    ```
    -eq -equal to
    -ne -not equal
    -gt -greater than
    -ge -greater or equal to
    -lt -lower than
    -le -lower or equal to

## Array, 'for' loops and other features of scripting in bash

- Exit codes are something similar to error handling into python or other language, once exit code is hit it will terminate the script and exit.
- In order to handle many arguments (or maybe user don't know the number of arguments that will be passed) there is way to handle this using built-in variable **$@**
- This brings us to the definitions of the array in bash, concept which uses other languages as well.
-In order to manage array and work with them, the concept of flow control and for look is a must to be introduced.

    ```bash
    #!/bin/bash

    if [ $# -eq 0 ];then                            # check if the number of arguments introduced is bigger than 0
        echo "Please enter at least one user."      
        exit 1                                      # exit code will exit the script and it can be checked by using echo $? command
    else
        for username in $@                          # for looks will check the list of the arguments introduced $@ is a built in variable 
        do
            echo $username |grep "^[A-Za-z]*$" >/dev/null   # here is a regular expression that check if the result contain only letters and will redirect the output to null file to be suppressed 
            if [ $@ -eq 1 ];then
                echo "ERROR: Names must only contains letters."
                exit 2
            else
                echo "Hello $username!"
            fi
        done
        exit 0                                      # exit code in case if the command successfully passed
    fi
    ```