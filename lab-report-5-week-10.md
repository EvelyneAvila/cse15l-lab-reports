# Lab Report 5 Week 10

In order to see the tests that were returning different outputs between the two implementations of markdown-parse (i.e. the one given in lab 9 vs my own implementation), I used `diff` on the results of running `bash script.sh` since we had previosly "sent" the results to a `results.txt` file.

![Image](diff.PNG)

* Note: In the results for `diff`, `<` is the CS Lab 9 implementation, and `>` is my own implementation 

## Test 1
This tests corresponds to file `22.md` where *neither* implementation is correct, as seen below:

**Actual outputs:**

![Image](lab-report-test1.PNG)

**Expected Output (according to [CommonMark demo site](https://spec.commonmark.org/dingus/))**

![Image](result1.PNG)

(where the expected outcome is `[ti\*tle]`)


In my own implementation of `markdown-parse`, while I check for a *new line* in between parenthesis, it fails to check for spaces within the parenthesis if they are in the same line (such as [x](a bc)), and take the last "word" between the parenthesis(i.e. "bc"). So we can correct this part of the program by fixing the code shown below in order for this test and similar cases to pass.

![Image](code-for-test1.PNG)

So in this case we can check is the string between the parenthesis contains a space, and if it does then obtain the last "word" in between parenthesis.


## Test 2
This implementation corresponds to file `41.md`, where the CS Lab 9 implementation is correct, as seen below:

**Actual outputs:**

![Image](lab-report-test21.PNG)


**Expected Output (according to [CommonMark demo site](https://spec.commonmark.org/dingus/))**

![Image](41.PNG)


In my own implementation, the bug that is presented in this test case is that we do not check for characters that are *definitive* when writing in .md files. This is because  `&quot;`  is read as `"`, and because of this special "command" then it's not a link. 

We can fix the bug by checking for this string in the file through an if statement and if it contains a "characteristic command" then we know it's not a link. We would need to do this for every "characteristic command" there is for .md files, and we can do so after the last if statement (shown below) that's inside the while loop in the `getLinks` method.

![Image](code-for-test1.PNG)