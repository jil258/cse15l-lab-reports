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


