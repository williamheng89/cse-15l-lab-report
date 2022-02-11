# Week 6 Lab Report

[Index](https://williamheng89.github.io/cse-15l-lab-report/index)

## Streamline SSH Configuration
**Trying to remember the command `ssh cs15lwi22zzz@ieng6.ucsd.edu` everytime we connect to our remote server is tedious and unecessary**

Instead, we can create an entry to tell SSH what username to use when logging into specific servers!

1. Open the .ssh folder in VS Code. This should be found with the directories: 

![Image](screenshots_LR3\configDirectory.png)


![Image](screenshots_LR3\openingSSHFolder.png)

2. Now create another file and entire the following:

```
Host ieng6
    HostName ieng6.ucsd.edu
    User cs15lwi22zzz (use your username)
```
After entering your username, it should look something like this:

![Image](screenshots_LR3\myConfigFile.png)

We're now done!

Upon creating a new terminal, we can connect to ieng6 with the command:
`ssh ieng6`

---

## Demonstration:

> Here I created a file and `scp` it to `ieng6` using our shortcut!

1. I copied the file over using our shortcut
2. I connected to ieng6 with our shortcut


![Image](screenshots_LR3\scpFileStreamLine.png)
