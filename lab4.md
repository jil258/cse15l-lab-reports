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

### Steps 6 - Run the tests, demonstrating that they fail
type bash test.sh to compile and run the java test
```
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

### Steps 7 - Edit the code file to fix the failing test

typing vim ListExamples.java ``<enter>`` to run vim for text editing
```
[cs15lfa23rs@ieng6-203]:lab7:77$ vim ListExamples.java
```

Keys pressed: /index1 ``<enter>``, n n n n n n n n n ``<right><right><right><right><right>`` x i 2 ``<esc>`` :wq \
The / is a search command in vim following by the texts we are searching which is index1 and n navigate through the occurences of the words, right tab 5 times get us to the 1 and x delete the 1. We enter insert mode with i and add 2 to the index and used ``<esc>`` to exit insert mode. Lastly with :wq we save and exit the vim.

### Steps 8 - Run the tests, demonstrating that they now succeed

Keys pressed: ``<up><up><enter>`` The bash test.sh is two commands up in the search history, so I used up arrow to access it. 
```
[cs15lfa23rs@ieng6-203]:lab7:78$ bash test.sh 
JUnit version 4.13.2
..
Time: 0.014

OK (2 tests)
```




