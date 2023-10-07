# Lab Report 1

## cd
1. **cd** with no argument
   ```
   [user@sahara ~]$ cd
   [user@sahara ~]$ ls
   lecture1
   [user@sahara ~]$ cd lecture1/
   [user@sahara ~/lecture1]$ cd
   [user@sahara ~]$
   ```
   * one on the home directory, one on the lecture1 directory
   * cd with no argument is default to home directory so running cd on home directory do nothing, and running on lecture1 directory directs us back to home directory.
   * no error
   
2. **cd** with a path to directory as an argument
   ```
   [user@sahara ~]$ cd lecture1/
   [user@sahara ~/lecture1]$
   ```
   * home
   * cd with a path to lecture1 directory brings us into the lecture1 folder
   * no error

3. **cd** with a path to a file as an argument
    ```
   [user@sahara ~]$ cd lecture1/messages/en-us.txt
    bash: cd: lecture1/messages/en-us.txt: Not a directory
   ```
   * home
   * cd with a path to en-us.txt file result in error
   * The error occurs since cd is shorten from change directory while en-us.txt is a file and not a directory.
  
## ls
1. **ls** with no argument
   ```
   [user@sahara ~]$ ls
   lecture1
   ```
   * home
   * ls show the directories and file inside the current directory. So lecture1 is currently inside home directory.
   * no error
     
2. **ls** with a path to directory as an argument
   ```
   [user@sahara ~]$ ls lecture1/
   Hello.class  Hello.java  messages  README
   ```
   * home
   * ls with a path to a directory show the directories and file inside that directory. So the four outputs are the files or directories living inside lecture1 directory.
   * no error
     
3. **ls** with a path to a file as an argument
   ```
   [user@sahara ~]$ ls lecture1/messages/en-us.txt
   lecture1/messages/en-us.txt
   [user@sahara ~]$ ls lecture1/Hello.class 
   lecture1/Hello.class
   ```
   * home
   * ls with a path to a file show the path to the file and do nothing since there are no file inside the file.
   * no error

## cat
1. **cat** with no argument
   ```
   [user@sahara ~]$ cat
   lecture1/messages/en-us.txt
   lecture1/messages/en-us.txt
   ```
   * home
   * When using cat command without any arguments, it reads from the standard input (keyboard) and displays the output to the standard output.
   * no error
     
2. **cat** with a path to directory as an argument
   ```
   [user@sahara ~]$ cat lecture1/
   cat: lecture1/: Is a directory
   ```
   * home
   * cat is not meant to display the contents of a directory,
   * Error: Attempt to use cat on a directory will result in an error since cat is meant to display contents of a file and not directory.
     
3. **cat** with a path to a file as an argument
   ```
   [user@sahara ~]$ cat lecture1/messages/en-us.txt 
   Hello World!
   ```
   * home
   * Using cat on a path to a file prints out the contents within the file.
   * no error
