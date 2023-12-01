### Debugging Scenario: Java Code with Merge Method

#### Title: Java merge Method Causing OutOfMemoryError

#### Post by Student

**Content:**
Hello, I'm encountering a problem with my merge method in ListExamples.java. This method is supposed to merge two sorted lists into a single sorted list. I wrote a JUnit test in ListTest.java to check its functionality. However, when I run my tests using the bash script test.sh, it throws an OutOfMemoryError. I suspect there might be an issue with the loops in the merge method, causing it to run indefinitely, but I don't know how to check the index values when my code does not produce any output. I will include screenshots showing the terminal output with the OutOfMemoryError during test execution, and the screenshot of my merge method. Could you please let me know how to track the increment of my indices during execution?

Screenshot: \
<img width="552" alt="Screenshot 2023-11-30 at 4 38 11 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/54f56cfc-7e82-4585-8b60-6586679bfa6a">

<img width="712" alt="Screenshot 2023-11-30 at 4 30 52 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/03b49948-0ef7-458d-afc9-ad4908791fcf">


#### Response from TA
**Content:**
It seems like your merge method might have an infinite loop causing the OutOfMemoryError. And it might be dued to falsly setting the indexing, if you want to track the index increment during the execution, you might consider adding print statements within the method to track the values of the indices and the state of the list at each iteration? \

**i.e.**
Inside the first while loop, after each if and else block, to track the values being added and the indices after each addition.
```
if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
    result.add(list1.get(index1));
    index1 += 1;
    // Add print statement here System.out.println("some context")
} else {
    result.add(list2.get(index2));
    index2 += 1;
    // Add print statement here System.out.println("some context")
}
```
Inside the second while loop, after the result.add() statement to monitor the remaining elements from list1 being added.
After adding these, please re-run your tests and share the output.
```
while (index1 < list1.size()) {

    // Add print statement here
    System.out.println("Finishing list1: " + some context);
}
```
Inside the third while loop, after the result.add() statement to monitor the remaining elements from list2 being added. Also, notice that in this loop there is a bug; it should increment index2 instead of index1.
```
Copy code
while (index2 < list2.size()) {
    // Add print statement here
    System.out.println("Finishing list2: " + some context);
}
```
By having all these print command, you should be able to spot which line of the code cause the infinity loop and make change accordingly. Please include any follow up question after you tried.

#### Follow-up Post by Student

**Content:**
I've added the print statements as suggested. I will include my changed code and the output from running the test script. Here's what the output shows. 

Screenshot/Terminal Output: \
<img width="463" alt="Screenshot 2023-11-30 at 5 10 40 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/623deb02-1851-4fa6-9df0-a8d5858bcb23">

Based on the output, I have determined that the issue is due to the fourth while loop, which is incrementing infinitely. It appears that index2 is not incrementing as expected, leading to an infinite loop. Therefore, I proceeded to change index1 to index2. After making this change, I received the correct output, and the test passed successfully. \
<img width="279" alt="Screenshot 2023-11-30 at 5 15 04 PM" src="https://github.com/jil258/cse15l-lab-reports/assets/102570197/515770c5-7f53-4776-9906-f7fbfc3d4fcd">

Content:
The debug output indicates an infinite loop in the merge method. It looks like the index2 is not incrementing correctly, causing the loop to add elements indefinitely and leading to OutOfMemoryError.

Debugging Scenario Setup
File & Directory Structure:

ListTest.java: Contains the JUnit test for the merge method.
ListExamples.java: Contains the merge method.
test.sh: Bash script to compile and run tests.
Contents of Each File Before Fixing the Bug:

ListTest.java: Test case for the merge method.
ListExamples.java: Contains the buggy merge method with incorrect loop logic.
test.sh: Script to compile and run tests.
Command Line to Trigger the Bug:

Run bash test.sh in the terminal.
Description of What to Edit to Fix the Bug:

In ListExamples.java, correct the loop that incorrectly increments index1 instead of index2.
This scenario showcases a complex bug involving infinite loops in Java, demonstrating the importance of careful loop condition handling and the use of debugging statements for problem resolution.

Run ./test.sh in the terminal.
Description of What to Edit to Fix the Bug:

In ListExamples.java, in the third while-loop, change index1 += 1; to index2 += 1;.
This correction will ensure that both lists are iterated through properly in the merge method.
