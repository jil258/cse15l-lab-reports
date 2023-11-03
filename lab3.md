# Lab Report 3

## Part1 List Methods
### A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
```
List<String> inputList = Arrays.asList("apple", "banana", "cherry");
List<String> filteredList = ListExamples.filter(inputList, sc);
        List<String> expectedList = Arrays.asList("apple", "banana");
        assertEquals(expectedList, filteredList);

testFilter(ListTests)
java.lang.AssertionError: expected:<[apple, banana]> but was:<[banana, apple]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at ListTests.testFilter(ListTests.java:20)
```

### An input that doesn’t induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
```
List<String> inputList2 = Arrays.asList();
        List<String> filteredList2 = ListExamples.filter(inputList2, sc);
        List<String> expectedList2 = Arrays.asList();
        assertEquals(expectedList2, filteredList2);

JUnit version 4.13.2
.
Time: 0.003

OK (1 test)
```


### The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)

The filter is intended to returns a new list that has all the elements of the input list for which the StringChecker returns true, and not the elements that return false, in
**the same order they appeared in the input list**. However the actual functionality do the StringChecker and add to the list in **Reverse order**.

The code produce expected output on a empty list and on a list with single element but can failed on a longer lists.
```
testFilter(ListTests)
java.lang.AssertionError: expected:<[apple, banana]> but was:<[banana, apple]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at ListTests.testFilter(ListTests.java:20)

JUnit version 4.13.2
.
Time: 0.003

OK (1 test)
```

### The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)

The fix made the adding to the end of the list instead of pushing from the front.
```
// Before:
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }

// After:
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }
```

## Part 2 - Researching Commands

grep command is what I choose since it is powerful when searching text using patterns. I have discover the below example through online search and combining the command on the used of the file in that we used in this week's lab.

#### Option 1: -i (Ignore case)
**Source ChatGPT, Prompt: pleas give a example of -i along with grep can be used during file search.** 
Output from ChatGPT: 
Option: -i (Ignore case)
The -i option in grep enables case-insensitive searching, which means it ignores the case of both the search pattern and the text in the file.

What -i Does
Using -i with grep allows you to find matches for a pattern regardless of whether it's written in uppercase, lowercase, or a mix of both. This is especially useful when the casing of the text isn't consistent or when you're unsure of it.

Example: Searching for "Error" in Any Case
bash
Copy code
grep -i "error" ./technical/server-logs.txt
In this example, grep will search for the word "error" in server-logs.txt within the ./technical directory, matching lines with "error", "Error", "ERROR", or any other combination of case.

**My Summary from Chatgpt output**
The -i option allows grep to perform case-insensitive searches. It's useful when the case of the text is unknown or it is a mix of uppercase and lowercase letters.

Example 1: Search for the word "network" regardless of case
grep -i "network" ./technical/config.txt
This command will find all occurrences of the word "network" in the file config.txt within the ./technical directory, ignoring whether it is typed as "Network", "NETWORK", or any other case variation.

Example 2: Search for the word "error" in all .log files
bash
Copy code
grep -i "error" ./technical/*.log
This searches for the word "error" in all .log files under the ./technical directory, ignoring case.



#### Option 2: -r (Recursive)
**Source ChatGPT, Prompt: pleas give a example of how to use -r along with grep to perform a recursive file search.** 
Output from ChatGPT: 
Option: -r (Recursive)
The -r (or --recursive) option allows grep to perform a recursive search. This means it will search through all directories and subdirectories starting from the given path.

What -r Does
When you use -r with grep, it will not only search within the specified directory but also in every subdirectory within it, applying the search pattern to every file it encounters.

Example: Recursively Searching for "config" in All Files
bash
Copy code
grep -r "config" ./technical/
In this example, grep will recursively search for the string "config" starting from the ./technical directory and continuing through all of its subdirectories, displaying every instance found.

Source: ChatGPT, Prompt: "please give an example of how to use -r along with grep to perform a recursive file search."

**My Summary from Chatgpt output**
The -r option allows grep to search recursively through directories, which means it will also search through all the subdirectories and their files.

Example 1: Recursively search for "admin" in all files
grep -r "admin" ./technical/
This command searches for the string "admin" in all files within the ./technical directory and its subdirectories.

Example 2: Recursively search for "timeout" in .conf files
grep -r "timeout" ./technical/*.conf
Even though the *.conf pattern is used, with the -r flag, grep will search for "timeout" in all .conf files in the directory and subdirectories.



#### Option 3: -v (Invert match)
**Source ChatGPT, Prompt: pleas give a example of how to use -v along with grep to do a file search.** 
Output from ChatGPT: 
Option: -v (Invert match)
The -v option inverts the match for the grep command, causing it to display lines that do not contain the specified pattern.

What -v Does
When you use -v with grep, it will filter and display all the lines in the input that do not match the given pattern. This is particularly useful when you want to exclude certain information from the search results.

Example: Excluding "passed" from Test Results
bash
Copy code
grep -v "passed" ./technical/test-results.log
In this example, grep searches through the file test-results.log in the ./technical directory. Instead of showing lines that contain the word "passed", it will show all lines that do not have the word "passed". This could be used to quickly find failed tests if the word "passed" is only used for successful test cases.

**My Summary from Chatgpt output**
The -v option inverts the match, showing only the lines that do not match the given pattern. It's useful when you want to exclude certain lines.

Example 1: Show lines that do not contain "success"
grep -v "success" ./technical/results-summary.txt
This command will output all lines from the file results-summary.txt that do not contain the word "success".

Example 2: Exclude lines with "deprecated" from search results
grep -v "deprecated" ./technical/upgrade-notes.md
This command filters out lines containing the term "deprecated" from the file upgrade-notes.md.



#### Option 4: --color (Color match)
**Source ChatGPT, Prompt: pleas give a example of how to use --color along with grep and what color match is doing.**
Output from ChatGPT: 
Option: --color
The --color option with the grep command highlights the matching text in the terminal. This feature enhances readability by making it easier to identify the matches at a glance.
What --color Does
When you use --color with grep, the matched text is displayed in a different color (usually red) in the terminal output. This colorization helps in quickly locating the strings that match the pattern within the sea of text.

**My Summary from Chatgpt output**
The --color option highlights the matching text. This can be extremely useful when I want to visually locate the matches quickly.

Example 1: Color-highlight "fail" in output
bash
Copy code
grep --color "fail" ./technical/error_report.txt
This will display the error_report.txt file's contents with the term "fail" highlighted in color.

Example 2: Highlight "critical" in red for visibility
bash
Copy code
grep --color "critical" ./technical/system_logs/*
This searches through all files within the system_logs directory for the word "critical" and highlights it in the output.

These options were found using the man grep command on a Linux system, which displays the manual pages for commands. Additionally, online resources such as Linux manual pages online and various Linux forums provide detailed explanations of these options.

Please note that the actual output from the commands isn't shown here, as these examples are hypothetical and I don't have access to your ./technical directory or its contents. If you have a specific directory or files you want to test these commands on, and they are accessible to me, I can run the commands and show you the actual output.

