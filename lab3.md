# Lab Report 3

## Part1 ArrayExamples reverseInPlace Method 
We want the method to changes the input array to be in reversed order

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
**A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)** 

One of the failure-inducing input in this case can be 
```
// input = {1, 2, 3} // Output: [3, 2, 3]

@Test
  public void testReverseInPlace_FailureCase() {
      int[] input = {1, 2, 3};
      ArrayExamples.reverseInPlace(input);
      assertArrayEquals(new int[]{3, 2, 1}, input);
  }
```

### An input that doesn’t induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
```
// input = {1} // Output: [1]

@Test
public void testReverseInPlace_SingleElement() {
    int[] input = {1};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{1}, input);
}
```


### The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)

The symptom reveals a flaw in the logic of the loop within the reverseInPlace method. Where it only works on a array with one element and not on those with one element and above. It indicates that the method is not iterating and swapping elements as intended for arrays with multiple elements. \
```
bash-3.2$ bash test.sh
JUnit version 4.13.2
.E.
Time: 0.005
There was 1 failure:
1) testReverseInPlace_FailureCase(ArrayTests)
arrays first differed at element [2]; expected:<1> but was:<3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace_FailureCase(ArrayTests.java:16)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more

FAILURES!!!
Tests run: 2,  Failures: 1
```

### The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)

The original implementation incorrectly tries to reverse the array by iterating over its entire length, which results in swapping the elements back to their original positions in arrays with more than one element. The fixed version correctly iterates only up to the midpoint of the array, swapping each element with its corresponding element from the other end. This approach ensures that each element is moved to its correct reversed position without being swapped back.

```
// Before:
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}

// After:
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
}
```

## Part 2 - Researching Commands

```grep``` command is what I choose since it is powerful when searching text using patterns. I have discover the below example through online search ChatGPT and using the man grep command on a Linux system, and combining the command on the used of the files structure that we used in this week's lab.

#### Option 1: -i (Ignore case)
**Source ChatGPT, Prompt: pleas give a example of -i along with grep can be used during file search.** \
Output from ChatGPT: \
Option: -i (Ignore case)
The -i option in grep enables case-insensitive searching, which means it ignores the case of both the search pattern and the text in the file.

What -i Does
Using -i with grep allows you to find matches for a pattern regardless of whether it's written in uppercase, lowercase, or a mix of both. This is especially useful when the casing of the text isn't consistent or when you're unsure of it.

Example: Searching for "Error" in Any Case
bash
Copy code
grep -i "error" ./technical/server-logs.txt
In this example, grep will search for the word "error" in server-logs.txt within the ./technical directory, matching lines with "error", "Error", "ERROR", or any other combination of case.

**My Summary from Chatgpt output:** \
The -i option allows grep to perform case-insensitive searches. It's useful when the case of the text is unknown or it is a mix of uppercase and lowercase letters.

Example 1: Search for the word "introduction" regardless of case \
```
> grep -i "IntroductIOn" .techincal/biomed/1468-6708-3-1.txt
        Introduction
```
This command will find all occurrences of the word "IntroductIOn" in the file biomed/1468-6708-3-1.txt within the ./technical/biomed directory, ignoring it is typed as "IntroductIOn" or any other case variation.

Example 2: Search for the word "error" in all .log files \
```
> grep -i "error" .techincal/biomed/*.txt
biomed/1468-6708-3-1.txt:        different. The bars are slightly offset to permit all error
biomed/1471-2091-3-17.txt:          inaccuracies in pH measurement produced serious errors in
biomed/1471-2091-3-31.txt:          standard error) in six experiments, three separate
biomed/1471-2091-3-31.txt:          Errors in molecular mass were propagated from standard
biomed/1471-2091-3-31.txt:          coefficient measurements. To calculate error in
biomed/1471-2091-3-31.txt:          assumption that all error in the molecular-mass
biomed/1471-2091-3-4.txt:        S values identical, within error, to
etc
```
This searches for the word "error" in all .txt files under the ./technical/biomed directory, ignoring case. \


#### Option 2: -r (Recursive) 
**Source ChatGPT, Prompt: pleas give a example of how to use -r along with grep to perform a recursive file search.** \
Output from ChatGPT: \
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

**My Summary from Chatgpt output** \
The -r option allows grep to search recursively through directories, which means it will also search through all the subdirectories and their files.

Example 1: Recursively search for "admin" in all files \
```
 ~/docsearch | main ?11  grep -r "admin" ./technical/   
./technical//biomed/ar104.txt:        paws. Similarly, administration of v-IL-10 into one knee of
./technical//biomed/ar104.txt:        v-IL-10, in that coadministration of adenoviral vectors
./technical//biomed/ar104.txt:        administered before onset of disease into knee joints,
./technical//biomed/1471-2202-2-2.txt:        of expressing foreign genes when administered in this
./technical//biomed/gb-2003-4-2-r8.txt:        administration and gene overexpression. The 
./technical//biomed/1471-2105-3-2.txt:            collected to assist in web server administration and
etc
```
grep -r "admin" ./technical/
This command searches for the string "admin" in all files within the ./technical directory and its subdirectories.

Example 2: Recursively search for "problem" in all txt files within biomed \
```
 ~/docsearch | main ?11  grep -r "problem" ./technical/biomed/*.txt          
./technical/biomed/gb-2001-2-12-research0055.txt:        intensity values are meaningless and problematic because
./technical/biomed/gb-2001-2-12-research0055.txt:          eliminates problematic negative values and retains
./technical/biomed/gb-2001-2-12-research0055.txt:          skew for the single problematic array will be removed
./technical/biomed/gb-2001-2-4-research0012.txt:        biological problems at multiple levels of abstraction (for
./technical/biomed/gb-2001-2-4-research0012.txt:          of linked icons. The problem for biologists is that
etc
```
Even though the *.txt pattern is used, with the -r flag, grep will search for "problem" in all .txt files in the directory and subdirectories. \

#### Option 3: -v (Invert match)
**Source ChatGPT, Prompt: pleas give a example of how to use -v along with grep to do a file search.** \
Output from ChatGPT: \
Option: -v (Invert match)
The -v option inverts the match for the grep command, causing it to display lines that do not contain the specified pattern.

What -v Does
When you use -v with grep, it will filter and display all the lines in the input that do not match the given pattern. This is particularly useful when you want to exclude certain information from the search results.

Example: Excluding "passed" from Test Results
bash
Copy code
grep -v "passed" ./technical/test-results.log
In this example, grep searches through the file test-results.log in the ./technical directory. Instead of showing lines that contain the word "passed", it will show all lines that do not have the word "passed". This could be used to quickly find failed tests if the word "passed" is only used for successful test cases.

**My Summary from Chatgpt output** \
The -v option inverts the match, showing only the lines that do not match the given pattern. It's useful when you want to exclude certain lines.

Example 1: Show lines that do not contain "success" \
```
grep -v "success" ./technical/911report/*.txt
./technical/911report/preface.txt:                this process with strong opinions about what would work. All of us have had to
./technical/911report/preface.txt:                pause, reflect, and sometimes change our minds as we studied these problems and
./technical/911report/preface.txt:                considered the views of others. We hope our report will encourage our fellow
./technical/911report/preface.txt:                citizens to study, reflect-and act.
./technical/911report/preface.txt:            Thomas H. Kean, chair
./technical/911report/preface.txt:            Lee H. Hamilton, vice chair
```
This command will output all lines from the file 911report/*.txt that do not contain the word "success".

Example 2: Exclude lines with "deprecated" from search results \
```
grep -v "deprecated" ./technical/911report/chapter-1.txt

    At 10:02 that morning, an assistant to the mission crew commander at NORAD's Northeast Air Defense Sector in Rome, New York, was working with his colleagues on the floor of the command center. In a brief moment of reflection, he was recorded remarking that "This is a new type of war."

    He was, and is, right. But the conflict did not begin on 9/11. It had been publicly declared years earlier, most notably in a declaration faxed early in 1998 to an Arabic-language newspaper in London. Few Americans had noticed it. The fax had been sent from thousands of miles away by the followers of a Saudi exile gathered in one of the most remote and impoverished countries on earth.
```
grep -v "deprecated" ./technical/911report/chapter-1.txt
This command filters out lines containing the term "deprecated" from the file chapter-1.txt. \

#### Option 4: --color (Color match)
**Source ChatGPT, Prompt: pleas give a example of how to use --color along with grep and what color match is doing.** \
Output from ChatGPT: \
Option: --color
The --color option with the grep command highlights the matching text in the terminal. This feature enhances readability by making it easier to identify the matches at a glance.
What --color Does
When you use --color with grep, the matched text is displayed in a different color (usually red) in the terminal output. This colorization helps in quickly locating the strings that match the pattern within the sea of text.

**My Summary from Chatgpt output** \
The --color option highlights the matching text. This can be extremely useful when I want to visually locate the matches quickly.

Example 1: Color-highlight "fail" in output \
```
grep --color "fail" ./technical/biomed/*.txt

./technical/biomed/gb-2003-4-7-r43.txt:          31.1) word pairs that failed the close spacing test
./technical/biomed/gb-2003-4-7-r43.txt:        which may fail to capture known binding sites. For example,
./technical/biomed/gb-2003-4-9-r57.txt:          lack may also explain our failure to find homologs of
./technical/biomed/rr167.txt:        conditions explains its failure to influence susceptibility
./technical/biomed/rr171.txt:        multi-organ failure and death [ 1 ] . Endotoxin-induced
./technical/biomed/rr196.txt:          strips suffered technical failure, leaving nine
```
This will display the *.txt file's contents with the term "fail" highlighted in color.

Example 2: Highlight "critical" in red for visibility \
```
grep --color "critical" ./technical/biomed/*

./technical/biomed/gb-2003-4-7-r42.txt:          loop appears to be the least critical feature of a
./technical/biomed/gb-2003-4-7-r46.txt:        plays a critical part in its development. However,
./technical/biomed/gb-2003-4-8-r51.txt:        is critical to the future development of these resources if
./technical/biomed/rr167.txt:        patients [ 18 ] . Of critical concern are 
./technical/biomed/rr167.txt:        B is also imparted by the absence or masking of critical
./technical/biomed/rr191.txt:        surfactant, which is critical for normal respiratory
```
This searches through all files within the biomed directory for the word "critical" and highlights it in the output.



