# Lab Report 4 - Vim (Week 7)

### Steps 4 - Log into ieng6
```
> ssh cs15lfa23rs@ieng6.ucsd.edu
Last login: Wed Nov 15 17:05:08 2023 from 100.81.34.58
Hello cs15lfa23rs, you are currently logged into ieng6-202.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   17:35:01   19  11.53,  12.58,  13.77
ieng6-202   17:35:01   17  1.50,   0.89,   0.60
ieng6-203   17:35:01   16  1.50,   1.59,   1.79

 
Wed Nov 15, 2023  5:35pm - Prepping cs15lfa23
[cs15lfa23rs@ieng6-202]:~:36$
```
Keys Pressed: I used the ```ssh cs15lfa23rs@ieng6.ucsd.edu``` + ```<Enter>``` which is my ieng login ID. As I already set the SSH keys so it doesn't requires me to type the password for it.

### Steps 5 - Clone your fork of the repository from your Github account (using the SSH URL)
```
[cs15lfa23rs@ieng6-202]:lab7-reports:43$ git clone git@github.com:jil258/lab7.git
Cloning into 'lab7'...
remote: Enumerating objects: 61, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 61 (delta 17), reused 15 (delta 14), pack-reused 34
Receiving objects: 100% (61/61), 376.
```
Keys Pressed: I first ```cd``` into lab7-reports which I created before and used ```git clone git@github.com:jil258/lab7.git``` + ```<Enter>``` command to clone the repository to my ieng6. The file here is folked to my Github account and now clone to my jeng6.

### Steps 6 - Run the tests, demonstrating that they fail

```
[cs15lfa23rs@ieng6-203]:~:74$ cd lab7
[cs15lfa23rs@ieng6-203]:lab7:75$ bash test.sh 
JUnit version 4.13.2
..E
Time: 0.539
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
        at ListExamples.merge(ListExamples.java:44)
        at ListExamplesTests.testMerge2(ListExamplesTests.java:19)

FAILURES!!!
Tests run: 2,  Failures: 1
```
Keys Pressed: I first used ```cd lab7```+ ```<Enter>``` to move into the directory. Then inside the directory, I ran the test.sh file with ```bash test.sh```+ ```<Enter>``` to run the test. Inside the test.sh, there is javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *java java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore
ListExamplesTests commands that compiles and runs the test file called ListExamplesTests

### Steps 7 - Edit the code file to fix the failing test

Key pressed: type ```vim ListExamples.java``` + ``<Enter>`` to run vim for text editing
```
[cs15lfa23rs@ieng6-203]:lab7:77$ vim ListExamples.java
```
<img width="863" alt="Screenshot 2023-11-28 at 1 21 56 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/4922ca8e-4d44-4ead-9912-e289baed8193">


from the lab I already know the bug is at line 44 so I typed ```:44``` + ```<Enter>```
<img width="588" alt="Screenshot 2023-11-28 at 1 21 37 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/19d1a363-65a1-4b72-9ec1-27a138291fbf">

It will jump to line 44 then by hitting the right 6 times ```<right><right><right><right><right><right>```. Hit ```i``` to enter insert mode. Hit ```<BackSpace>``` to delete 1 and hit 2 to fix the bug. Then hit ```ESC``` to exit the insert mode and go back to normal mode.

<img width="507" alt="Screenshot 2023-11-28 at 1 24 08 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/fa830428-8f47-41c7-ac9f-df19f1996fec">

After fixing type ```:wq``` + ```<Enter>``` to save and exit

### Steps 8 - Run the tests, demonstrating that they now succeed

Keys pressed: ```bash test.sh``` + ```<Enter>``` to run the test.
```
[cs15lfa23rs@ieng6-203]:lab7:78$ bash test.sh 
JUnit version 4.13.2
..
Time: 0.014

OK (2 tests)
```

### Steps 9
Key Pressed: In here, I first add the changes to the git by ```git add .``` + ```<Enter>``` and then use the
command ```git commit -m "fix bug"``` + ```<Enter>``` to commit the file. Option -m allows us to type the message inside the
terminal. And I used ```git push``` + ```<Enter>``` to successfully push our changes to the git and Github repository in my account
```
[cs15lfa23rs@ieng6-202]:lab7:109$ git add .
[cs15lfa23rs@ieng6-202]:lab7:110$ 
[cs15lfa23rs@ieng6-202]:lab7:110$ git commit -m "fix bug"
[main 8cd967a] fix bug
 Committer: Jian-Peng Li <cs15lfa23rs@ieng6-202.ucsd.edu>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+), 1 deletion(-)
[cs15lfa23rs@ieng6-202]:lab7:111$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 297 bytes | 297.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:jil258/lab7.git
   d0edb07..8cd967a  main -> main
[cs15lfa23rs@ieng6-202]:lab7:112$ 
```




