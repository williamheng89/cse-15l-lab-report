# Week 8 Lab Report 
## Code Review

To make things easier, I copied the reviewed code into my repository and created another test file for it. Then I updated the Makefile to run the JUnit tester on the file I was to review. 

[Link to my Repository](https://github.com/williamheng89/markdown-parse)

Adding Tests for snippets 1-3

![Image](screenshots_LR4\myTester.png)

Actual Output:

 ![Image](screenshots_LR4\myFailedTests.png)


[Link to Reviewed Code Repository](https://github.com/leo3friedman/markdown-parse)

Adding Tests for snippets 1-3

![Image](screenshots_LR4\fixTester.png)

Actual Output:

![Image](screenshots_LR4\fixFailedTests.png)

## Reflection: Potential Solutions?

`Snippet 1`
It is possible for a small (<10 lines) code change that will enable my program to work for all related cases of inline code with backticks, however, it is impossible for the small change to work for all of snippet-1. This is because snippet-1 contains an imbedded close bracket and my current program does not cover that. I will need to adjust my code even more.

`Snippet 2`
There is no small (<10 lines) code change that will enable my program to work for all cases that contain nested parenthesis, brackets, and escaped brackets. I believe I would need to implement a system that grabs potential links, those that have weird nested behaviors, and also create new variables to hold temporary indexes. After this, I would still need to adjust my program to dissect those potential links. Overall, I will need to add a large portion of code to make this work. 

`Snippet 3`
There is no small (<10 lines) code change that will enable my program to work for all cases that have newlines in brackets and parentheses. My program already contains flaws, using lots of return statements that cause trying to grab the long links return early, hence it grabbed 0 links. Because of this, I would need to change a handful of these lines in addition to implementing a system that handles newlines. This would require changing a large portion of my program, in addition to adding much more. 
