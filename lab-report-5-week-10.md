# Week 10 Lab Report
## Comparing Two Differing Implementations:

**How to find the tests with differing results?**

1. I edited the script.sh file so that right before our `java MarkdownParse (some file name)` command is ran, it echos the file name.

![Image](screenshots_LR5\scriptshFile.png)

2. Now after calling `bash script.sh`, it prints out the file name before the getLinks output. We can now use the command `bash script.sh > results.txt` . What this does is run our bash command, it redirects its output into a file called "results.txt" rather than the terminal (it also deletes and recreates ths target file evertime the command is run.

3. Now using a Visual Studio Extension called Remote Explorer or the command `cat results.txt` we can see our output stored in a text file.

![Image](screenshots_LR5\outputRedirection.png)

4. We then do the same with our MarkdownParse repo: copy over the `script.sh` file and run `bash script.sh > results.txt` . After doing so, we now have 2 text files that contain an understandable list of getLinks outputs. 

5. We now can use thr program diff to show the differences between the outputs of our programs: `diff markdown-parse/results.txt WHmarkdown-parse/results.txt` . We should see something like this. To undersstand the output, the 212 of the results.txt in the markdown-parse directory, the line contains [url], however, the 212 of the WHmarkdown-parse directory contained []. 

![Image](screenshots_LR5\diffOutputs.png)

6. However, these lines don't exactly tell us what files are making our getLinks implementations have differing outputs. To see this, I am using the VS Code Remote Explorer extension to view the line numbers to find the names of the test-files. As seen below, line 212 is test-files/194.md getLinks output. 

![Image](screenshots_LR5\remoteExplorer.png)

---

**Now what we're able to figure out which tests have differing results, we can dive into which implementation is correct or if both are incorrect**

1. A test from the 652 commonmark-spec tests where our differing implementations had differing outputs was with line 230 in results.txt which translates to test-files/210.md

![Image](screenshots_LR5\error201.png)

Both Outputs:

![Image](screenshots_LR5\bothOutputs.png)

To see what the correct output is, I copied and pasted into [the common mark demo](https://spec.commonmark.org/dingus/)

![Image](screenshots_LR5\1correctOutput.png)

As shown, no links were grabbed and thus the output should be an empty list. However, the actual output was:

```
baz
```

This shows that the markdown-parse implementation provided in Lab 9 was incorrect. Interestingly Commonmark is able to grab links following a complete square bracket pair followed by a colon. 

![Image](screenshots_LR5\interestingFind.png)

However it does not grab links if there is a "<" symbol found after the colon. Thus the bug in this implementation is that it does not search if the first character in a continuous sequence leading to the parenthesis is "<". This fix can be made in between lines 64 and 65.

![Image](screenshots_LR5\solution1.png)

2. Another test from the 652 commonmark-spec tests where our differing implementations ahd differing outputs was with line 542 in results.txt which translates to test-files/342.md

![Image](screenshots_LR5\error342.png)

Both Outputs: 

![Image](screenshots_LR5\bothOutputs.png)

After running this file's contents through the markdown demo, it is seen that no links should be grabbed:

![Image](screenshots_LR5\2correctOutput.png)\

As shown, no links were grabbed and thus the output should be an empty list. However, the actual output was:

```
/foo`
```

This shows that the markdown-parse implementation provided in Lab 9 was incorrect. Interestingly Commonmark is able to grab this link had it not contained a back quote inside the square brackets

![Image](screenshots_LR5\interestingFInd2.png)

With that being said, the the bug in this implementation is that it does not search if a back quote character is contained inside the square brackets. This fix can be made after line 73 (after finding the indexes of both square  brackets and making sure that they both exist: we do not want an index out of bounds exception)

![Image](screenshots_LR5\solution2.png)