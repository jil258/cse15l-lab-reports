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
   * the error occurs since cd is shorten from change directory while en-us.txt is a file and not a directory.
  
## ls
1. **ls** with no argument
2. **ls** with a path to directory as an argument
3. **ls** with a path to a file as an argument

## cat
1. **cat** with no argument
2. **cat** with a path to directory as an argument
3. **cat** with a path to a file as an argument
