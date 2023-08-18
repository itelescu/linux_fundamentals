## Specific commands on linux distribution

- Open GUI folder or file on indicated path:
    ```
    nautilus /home/iontelescu/Desktop/Linux
    xdg-open <filename>
    ```

- Funny packages:
    ```
    sudo apt install cowsay     - install cowsay package
    sudo apt install figlet     - install figlet package
    sudo remove cowsay          - remove cowsay package
    sudo apt purge cowsay       - remove cowsay cash package
    sudo apt purge figlet       - directly remove package and its cash
    ```
- In order to display the file structure of current file, use:
    ```
    tree        - display the structure of the file tree
    find        - display all file of current directory
    ls -t -r    - will display the files/directories in reversed order by creation
    ```
- Open google chrome in background can be done by 2 commands:
    ```
    nohup google-chrome &
    google-chrome & disown
    ```
- To clean-up the content of the file and to write more lines to a file:
    ```
    >filename                           - filename will be wiped-up
        
    cat << delimiter_word > file_name   - write the content until delimiter_word occur into a file
    ```
- To cut specific columns from a file or a text content use cut command:
    ```
    file_content.txt
    John:Doe:25:Male
    Jane:Smith:30:Female
    Alice:Johnson:28:Female

    cut -d ':' -f 2 file_content.txt    - this command will display second name from each line, -d is delimiter and -f is the field number
    ```