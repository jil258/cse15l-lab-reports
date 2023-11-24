### 1
Create the following directory structure within the /home/student/ directory (the default directory the terminal starts in):

```
cd step1
mkdir source lib data
touch source/Main.java lib/Library.java
cd data
mkdir 2022 2023
touch 2022/data.csv 2023/data.csv
```

### 2
The directory in the workspace called project is a git repository. Add a new file in that directory called README and make a commit that adds that file to the repository, where the commit message contains the string skill demo. (You don't have to push the commit anywhere, and the README file can have any content you like)

```
touch README
git add README
git commit -m "skill demo"
```

### 3
The directory called buggy has a file called ListExamples.java that has bugs in the filter and merge implementations. Run the tests and put the failing output from JUnit in a file called test-fail-output.txt in the home directory (e.g. into /home/student/test-fail-output.txt.

```
bash test.sh > /home/student/test-fail-output.txt
```

### 4
Then, fix the bugs in the ListExamples.java program and rerun the tests to demonstrate that it worked. Put the successful test output in a file called test-success-output.txt in the home directory.

```
vim ListExamples.java

//change
result.add(s);

//change index1 -> index2
while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }

:wq

bash test.sh > /home/student/test-succes-output.txt
```

### 5
Make a commit that has your edits to fix the bug in the buggy directory. The commit message should contain the string fix bugs.

```
git add .
git commit -m "fix bugs"
```

### 6
The directory called jBCrypt has an open-source implementation of an encryption algorithm called password hashing in the file BCrypt.java, and a Main class that has an example of hashing a password with a command-line argument. You don't need to understand the details of the algorithm to answer this question. Assume that we run the program with:
java Main mypassword
```
javac -g *.java         //inside jBCrypt directory
jdb Main mypassword
stop at BCrypt:686
run
print hashed.length    // hashed.length = 24
quit
cd ..
touch hashed.txt
vim hashed.txt
i
24
:wq
```
