#  Week 2 Lab Report
## Installing VS Code
* Go to the [Visual Studio Code](https://code.visualstudio.com/) Website
* Follow the instructions to downloand and install. Make sure to choose the version for your OS

After installing, you should be able to open a window that looks like so:
![Image](screenshots/installing_vscodeSC.png)

---
## Remotely Connecting
* Open Settings > Apps > Apps & Features > Optional Features and scan if OpenSSH is already installed. If not, [install OpenSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
* [Find your course-specific account for the class](https://sdacs.ucsd.edu/~icc/index.php)
* To begin connecting to our remote host, open VS Code > Terminal > New Terminal (creating a terminal) and enter the command (replace `zz` with your course specific account):

 `ssh cs15lwi22zz@ieng6.ucsd.edu`


* When a message pops up asking to continue, type and enter `yes`
* Enter your password when asked (you will not see any placeholders)

After doing so, you should see a message like so:

![Image](screenshots/remotelyconnectionSC.png)

---
## Trying Some Commands

Go ahead and try out some commands!
> `ls -h` : lists human readable files


> `cat <file name> `: prints out contents within that file


> `cd <directory>` : changes directories

Since I have files in the server under my course account, I can do something like this!

![Image](screenshots/trying_some_commandsSC.png)

To log yourself out of the servier, use:

> Type `exit` in the terminal

![Image](screenshots/logoutSC.png)

---
## Moving Files with `scp`
* Create a file called `WhereAmI.java` in your VS Code
* Copy and Paste the following:

``` 
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

* Save and run the file using `javac WhereAmI.java` followed by `java WhereAmI`

As we run this program locally (on our computer), we should see the name of our OS, username, home, and directory of this file.

![Image](screenshots/WhereAmISC.png)


* Now from the directory where this file is made, enter the command `scp WhereAmI.java cs15lwi22zz@ieng6.ucsd.edu:~/` (remember to change the `zz`) and login

You have now `scp`(secure copied) this file onto the host.


* Use the `ls -h` command and you can see that the file has been copied onto the home directoy
* Use the same `javac` and `java` commands

![Image](screenshots/scpSC.png)

As you can see, what's printed is the program running on the server, thus it is different than when we ran it on our client.

---
## Setting an SSH Key
Inputting your password everytime you login to a remote server can be annoying. Thus, we can copy files on our local client and onto the server to recognize our login to remove the need of typing our password.

* Open up your command prompt and enter `ssh-keygen`
* Save it under  `/Users/willi/.ssh/id_rsa` be sure to replace `willi` with your username
* Leave the passphrase empty (press enter)

You should now see this:

![Image](screenshots/keygenSC.png)


* If you are on Windows, follow these [ssh-add](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation) steps


 Connect with the remote host and use the command `mkdir .ssh` then `exit`
![Image](screenshots/keygen_mkdirSC.png)


* On your client use the command `scp /Users/willi/.ssh/id_rsa.pub cs15lwi22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys` (replace `willi` with your username and `zz` with your account).


* Enter your password and now you can connect w/o inputting your password!

![image](screenshots/successful_keygenSC.png)

---
## Optimizing Remote Running
Setting an SSH key is one prime example of making remote running more effecient and cutting down repetitive tasks. Here are some other tricks to further eliminate repetition.

* If we just exited our remote host, we can use the `up arrow key` to look for previous commands. This is so that we don't have to keep typing out that command or even copy/paste
* We can even run commands at the end of an `ssh` by wrapping it in `quotations`.


![Image](screenshots/OptimizingSC.png)



* With this in mind, we can also use `;` to run multiple commands

![Image](screenshots/multiple_commandsSC.png)


* **Check this out!** After editing and saving the WhereAmI.java file, we are able to copy, compile, and execute our updated program onto the remote server with just 6 keystrokes!

![Image](screenshots/CountingKeyStrokesfix.png)

`scp WhereAmI.java cs15lwi22aaq@ieng6.ucsd.edu:~/ = 3`
> (Up-arrow + Up-arrow + Enter)  

`ssh cs15lwi22aaq@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI" = 3`
> (Up-arrow + Up-arrow + Enter) 

`It is possible to do this with 6 keystrokes only if these commands were ran prior (in order to use "up-arrow" shortcut)`
