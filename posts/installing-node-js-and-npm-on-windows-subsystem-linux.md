# Installing Node.js and NPM on Windows Subsystem Linux
---

### UPDATE
I found a program called [ConEmu](https://conemu.github.io/) that acts as a front-end terminal that sits on top of what ever shells you want to use.  It let me use it as a front-end for WSL, giving me the ability to fix a few problems, like using my custom color theme, giving me tabs for multiple ubuntu windows, and TMUX's borders being drawn incorrectly.
 
 I am now currently using an XPS 13 as my main dev machine, and am currently very happy with the workflow of being able to use WSL Ubuntu, along with the extended functionality that ConEmu is providing me, as well as having the super portability of a small/light laptop.
 
 ### UPDATE 2
 So after extensive use of conEmu as a front face for Ubuntu WSL, you can notice a refresh delay.  Almost as though you can tell ConEmu is connected to Ubuntu via wslbridge, and you can feel the latency from that.
 I found a way to get past this though.  So, rather than have conEmu open legit ubuntu tabs `{Bash::bash}`, I instead am having conEmu open a regular `cmd.exe` window (beause it runs faster), and then am starting `bash.exe` within that window, effectively still getting my Ubuntu WSL.  With the `/C` switch, you can tell cmd.exe to run a command upon starting up.  So, I have created a new custom 'task' on conEmu (a new shell choice pretty much), and told it to start this as my shell: `cmd.exe /C bash.exe`, and made it my default startup shell when I open a new tab.  The screen updates/refresh rate/what ever you might want to call it - seems to be running noticeably faster.

---


### Original Post
Today I ran through quite a bit of trouble getting the most current versiosn of nodejs and npm installed in my Ubuntu 18 (on windows 10).

It turns out, the normal way of using apt-get to install it, installs a pretty old version.  The workaround, I found on a [github gist here](https://gist.github.com/micahgodbolt/8b9a338c8bab7bc147975646ea20826c).

```
$ touch ~/.bashrc
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
// restart bash
$ nvm install node
```
(note, for the 1st line to create a `.bashrc` file, mine already existed, so I skipped that line).

These are the lines that it adds into your .bashrc file:
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

(another note, on a ubuntu 18 machine, for some reason the lines that were inserted into the .bashrc file weren't working, so I copy/pasted them out of `.bashrc` into `.bash_profile` and things worked correctly from there.)

(note again, it seems these additional lines added to your startup makes bash start significantly slower... So what I have done is commented them out, and will only re-enable them when I need to use NVM, and will comment them back out when I'm done with NVM.)

It's a simple curl command that will download and run a bash script that will install NVM (Node Version Manager), and then you use NVM to install the latest and greatest node and npm.

Here is the actual github page for nvm itself, if you're curious:
[https://github.com/creationix/nvm/blob/master/README.md](https://github.com/creationix/nvm/blob/master/README.md)

As of writing this article, this worked for me, and I was able to proceed working on my angular project originally started on my Macbook Pro.
